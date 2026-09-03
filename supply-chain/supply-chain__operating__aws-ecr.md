<!-- source: https://www.opswat.com/docs/supply-chain/operating/aws-ecr -->

# AWS ECR

## AWS Lambda with Amazon ECR trigger for automatic MDSSC container scanning

This guide explains how to automatically scan a container image in MetaDefender Software Supply Chain (MDSSC) when it is pushed to Amazon Elastic Container Registry (ECR).

When an image is pushed, Amazon EventBridge invokes an AWS Lambda function. The function calls the MDSSC API to start a scan for the pushed repository and tag, which is then processed by MetaDefender Core through your MDSSC scan pool.

## How it works

```text
Push image -> Amazon ECR -> EventBridge rule -> AWS Lambda -> MDSSC API (/jobs) -> MetaDefender Core -> verdict
```

ECR emits an ECR Image Action event on every push. An EventBridge rule matches successful pushes and invokes the Lambda. The Lambda reads the repository and tag from the event and starts an MDSSC scan for that specific tag.

## Prerequisites

- A running MDSSC instance that AWS Lambda can reach over HTTPS (public endpoint, or Lambda in a VPC with network access to MDSSC).
- An MDSSC user with permission to create connections and API keys.
- A MetaDefender Core scan instance registered in your MDSSC MD Core scan pool.
- An AWS account with the target ECR repositories, and permissions to create IAM roles/users, Lambda functions, Secrets Manager secrets, and EventBridge rules.
- An IAM user with ECR read access. MDSSC's ECR connection requires a long-lived access key and secret (temporary STS credentials are not supported).

## Step 1 - Create an IAM user with ECR read access (for the MDSSC connection)

MDSSC pulls image metadata and layers from ECR using an access key you provide. Create a dedicated IAM user, attach the AWS managed policy `AmazonEC2ContainerRegistryReadOnly` (or the equivalent below), and create an access key pair.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ecr:GetAuthorizationToken",
        "ecr:BatchCheckLayerAvailability",
        "ecr:GetDownloadUrlForLayer",
        "ecr:BatchGetImage",
        "ecr:DescribeRepositories",
        "ecr:DescribeImages",
        "ecr:DescribeRegistry",
        "ecr:ListImages"
      ],
      "Resource": "*"
    }
  ]
}
```

Save the **Access key ID** and **Secret access key** — you will enter them in MDSSC in the next step.

## Step 2 - Configure MDSSC (ECR connection, scan instance, API key)

1. In MDSSC, add an **Amazon ECR connection** using the access key from Step 1 and the AWS region of your registry. Give it a memorable **name** (for example, `MDSSC ECR`) — you will need this name and the connection's **Storage ID** for the Lambda.
2. Ensure a **MetaDefender Core scan instance** is registered in the default MD Core scan pool. Adding it enables MDSSC to scan images from this connection.
3. Generate an **API key** for the account the Lambda will use. This key is sent in the `apikey` request header.

Find the connection **Storage ID** via the MDSSC API (`GET /api/v1/services`) or the connection details page.

## Step 3 - Store the MDSSC API key in AWS Secrets Manager

Create a secret so the Lambda does not hard-code the key. Store it as JSON:

```json
{ "apikey": "<your-mdssc-api-key>" }
```

Note the secret ARN for Step 5.

## Step 4 - Create the IAM execution role for Lambda

Create a role that Lambda can assume (trusted service `lambda.amazonaws.com`). Attach `AWSLambdaBasicExecutionRole` (CloudWatch Logs) plus an inline policy so the function can read the secret:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["secretsmanager:GetSecretValue"],
      "Resource": "<your-secret-arn>"
    }
  ]
}
```

If you configure a dead-letter queue (optional), add the relevant SQS permissions for your queue ARN.

## Step 5 - Create the Lambda function

1. Go to AWS Lambda - Create function - Author from scratch.
2. Runtime: Python 3.x. Execution role: the role from Step 4.
3. (Optional) Under Configuration - Asynchronous invocation, configure retries and a dead-letter queue (SQS) if you want to retain failed events for troubleshooting.

## Step 6 - Deploy the Lambda code

Paste the following into the function and deploy. It parses the ECR push event, builds the MDSSC repository ID, and starts a scan of the pushed tag.

> **TLS verification**
>
> Set `VERIFY_TLS=true` in production so the Lambda verifies the MDSSC TLS certificate. Use `VERIFY_TLS=false` only for test environments with self-signed certificates.

```python
import base64, json, os, ssl, urllib.request
import boto3

_secrets = boto3.client("secretsmanager")
_apikey = None

def _get_apikey():
    global _apikey
    if _apikey is None:
        raw = _secrets.get_secret_value(
            SecretId=os.environ["MDSSC_SECRET_ARN"]
        )["SecretString"]
        try:
            _apikey = json.loads(raw).get("apikey", raw)
        except json.JSONDecodeError:
            _apikey = raw
    return _apikey

def _ssl_ctx():
    if os.environ.get("VERIFY_TLS", "true").lower() == "true":
        return None
    ctx = ssl.create_default_context()
    ctx.check_hostname = False
    ctx.verify_mode = ssl.CERT_NONE
    return ctx

def _repository_id(connection_name, account, region, repo):
    arn = f"arn:aws:ecr:{region}:{account}:repository/{repo}"
    return base64.b64encode(f"{connection_name}/{arn}".encode()).decode()

def handler(event, _context):
    detail = event.get("detail", {}) or {}
    if detail.get("action-type") != "PUSH" or detail.get("result") != "SUCCESS":
        return {"skipped": True}

    account = event["account"]
    region = event["region"]
    repo = detail["repository-name"]
    tag = detail.get("image-tag") or "latest"

    conn = os.environ["MDSSC_CONNECTION_NAME"]
    storage_id = os.environ["MDSSC_STORAGE_ID"]
    rid = _repository_id(conn, account, region, repo)

    payload = {
        "Name": f"ecr-{repo}-{tag}",
        "Priority": "Low",
        "ReferenceSelectionMode": "Specific",
        "Targets": [
            {
                "StorageId": storage_id,
                "RepositoryId": rid,
                "RepositoryName": repo,
                "ReferenceSelectionMode": "Specific",
                "References": [tag],
            }
        ],
    }

    url = os.environ["MDSSC_URL"].rstrip("/") + "/api/v1/jobs"
    req = urllib.request.Request(url, data=json.dumps(payload).encode(), method="POST")
    req.add_header("Content-Type", "application/json")
    req.add_header("apikey", _get_apikey())

    with urllib.request.urlopen(req, timeout=30, context=_ssl_ctx()) as r:
        print("MDSSC", r.status, r.read().decode("utf-8", "replace"))

    return {"ok": True, "repo": repo, "tag": tag}
```

## Step 7 - Configure environment variables

| Variable | Description | Example |
| ---- | ---- | ---- |
| `MDSSC_URL` | Base URL of your MDSSC instance | `https://mdssc.example.com` |
| `MDSSC_STORAGE_ID` | ID of the ECR connection created in Step 2 | `019fa810-4ef3-…` |
| `MDSSC_CONNECTION_NAME` | Name of the ECR connection (Step 2) | `MDSSC ECR` |
| `MDSSC_SECRET_ARN` | ARN of the Secrets Manager secret (Step 3) | `arn:aws:secretsmanager:…` |
| `VERIFY_TLS` | Set to `true` to verify the MDSSC TLS certificate. Leave `false` for self-signed certificates. | `false` |

## Step 8 - Configure the Amazon ECR (EventBridge) trigger

ECR image actions are delivered to the default EventBridge bus automatically — no configuration is needed on the ECR side. Create a rule that matches successful pushes and targets your Lambda.

1. Go to **Amazon EventBridge → Rules → Create rule** (default event bus).
2. 2. Choose Rule with an event pattern and paste:
   ```json
   {
     "source": ["aws.ecr"],
     "detail-type": ["ECR Image Action"],
     "detail": { "action-type": ["PUSH"], "result": ["SUCCESS"] }
   }
   ```

3. Set the **target** to your Lambda function and create the rule. EventBridge adds the invoke permission automatically.

To scan only specific repositories, add `"repository-name": ["repo-a", "repo-b"]` inside `detail`.

## Step 9 - Test

1. Push (or re-tag) an image to one of the target ECR repositories:

   `docker tag alpine:3.20 <account>.dkr.ecr.<region>.amazonaws.com/<repo>:demo`
   `docker push <account>.dkr.ecr.<region>.amazonaws.com/<repo>:demo`
2. In **CloudWatch Logs** for the function, confirm a line like `MDSSC 200 {"Result":"Success","ResponseMessage":"Job started"}`.
3. In the MDSSC UI, open **Scans / Jobs** and confirm a new scan for `<repo>:demo` appears and completes.

## **Notes and troubleshooting**

- **Per-tag vs latest:** the function scans the exact pushed tag because it sets `ReferenceSelectionMode: "Specific"`. If you remove that, MDSSC scans the `:latest` tag by default.
- **Identical images are de-duplicated:** pushing a new tag that points to an already-scanned image digest reuses the existing result instead of re-pulling.
- **Connectivity:** if the function times out, verify Lambda can reach the MDSSC URL (security groups / VPC / public endpoint).
- **Authorization errors:** confirm the `apikey` secret is correct and the ECR connection credentials have the read permissions in Step 1.
- **Resilience:** configure the Lambda dead-letter queue so transient failures can be retried or inspected.
