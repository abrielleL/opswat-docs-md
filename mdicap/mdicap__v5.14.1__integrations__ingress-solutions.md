<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/ingress-solutions -->

# NGINX Ingress Controller Integration

## [OMetaScan NGINX Ingress Controller Configuration](/docs/mdicap/v5.14.1/integrations/ingress-solutions#ometascan-nginx-ingress-controller-configuration)

**This document covers the new approach** using the OPSWAT-customised image on top of the NGINX Ingress Controller Helm chart ([maintained by NGINX Org](https://github.com/nginx/kubernetes-ingress)). For the Kubernetes Ingress Controller (EOL March 2026), starting from version of the controller 5.4.2 will be compatible with the Ingress Controller provided by NGINX Org.

### [ConfigMaps](/docs/mdicap/v5.14.1/integrations/ingress-solutions#configmaps)

ConfigMaps allow you to decouple configuration artifacts from image content to keep containerized applications portable.

The ConfigMap API resource stores configuration data as key-value pairs. The data provides the configurations for system components for the nginx-controller.

| **Name** | **Type** | **Default** | **Usage** |
| --- | --- | --- | --- |
| enable-ometascan | bool | “false” | Enable or Disable ometascan module globally  **Note**: You must enable this config to use ometascan module |

### [Annotations](/docs/mdicap/v5.14.1/integrations/ingress-solutions#annotations)

| **Name** | **Type** | **Default** | **Usage** |
| --- | --- | --- | --- |
| nginx.org/ometascan-send-timeout | number | 60 | Sets a timeout for transmitting a request to the proxied server. The timeout is set only between two successive write operations, not for the transmission of the whole request. If the proxied server does not receive anything within this time, the connection is closed. |
| nginx.org/ometascan-read-timeout | number | 86400  (1 day) | Defines a timeout for reading a response from the proxied server. The timeout is set only between two successive read operations, not for the transmission of the whole response. If the proxied server does not transmit anything within this time, the connection is closed. |
| nginx.org/ometascan-pre-cache-size | number | `9223372036854775807`  (maximum number of Nginx) | Config maximum caching size per request. |
| nginx.org/ometascan-pre-cache | "true" or "false" | "false" | Turn on/off pre-caching request when sending to ICAP Server |
| nginx.org/ometascan-pass | string | No default | Sets the protocol and address of a ICAP server and an optional URI to which a location should be mapped.  e.g: <http://icap-address:8043>  **Note**: Must have it for enable annotation |
| nginx.org/ometascan-methods | string | GET HEAD POST PUT PATCH DELETE | This directive specifies HTTP request methods that are considered by `ometascan_pass`. HTTP request methods not listed will be skipped completely. The following HTTP methods are allowed: `GET`, `HEAD`, `POST`, `PUT`, `PATCH`, and `DELETE` |
| nginx.org/ometascan-connect-timeout | number | 60 | Defines a timeout for establishing a connection with a proxied server. It should be noted that this timeout cannot usually exceed 75 seconds. |
| nginx.org/ometascan-x-forwarded-for | string | off | Parse X-Forwarded-For for client IP |
| nginx.org/ometascan-intercept-errors | string | off | Intercept error responses for scanning |
| nginx.org/ometascan-allow-bad-request-traffic | string | off | Allow traffic on ICAP bad request |
| nginx.org/ometascan-set-header | string |  | Custom headers to send to ICAP (multi-line) |
| nginx.org/ometascan-ssl-trusted-certificate | string |  | CA secret reference (`namespace/name`) |
| nginx.org/ometascan-ssl-ciphers | string | DEFAULT | SSL ciphers |
| nginx.org/ometascan-ssl-protocols | string | TLSv1.2 TLSv1.3 | SSL protocols |
| nginx.org/ometascan-ssl-name | string | $proxy_host | SSL server name |
| nginx.org/ometascan-ssl-verify | number | 1 | Certificate chain depth |
| nginx.org/ometascan-ssl-server-name | string | off | Enable SNI |
| nginx.org/ometascan-ssl-session-reuse | string | on | SSL session reuse |
| nginx.org/ometascan-health-check | string | The annotation enables active health checking of the MD ICAP Server upstream. When enabled, NGINX periodically probes the ICAP server and automatically marks it UP or DOWN based on the results. Requests are not sent to servers marked DOWN. E.g: nginx.org/ometascan-health-check: "interval=<ms> [passes=<n>] [fails=<n>] [timeout=<ms>] [jitter=<ms>] [mandatory [persistent]]" |  |

You can add these Kubernetes annotations to specific Ingress objects to customize their behavior.

## [OMetaScan NGINX Ingress on Minikube](/docs/mdicap/v5.14.1/integrations/ingress-solutions#ometascan-nginx-ingress-on-minikube)

### [Requirement](/docs/mdicap/v5.14.1/integrations/ingress-solutions#requirement)

- Minikube: <https://minikube.sigs.k8s.io/docs/>
- NGINX Ingress with OMetascan module images on [Docker Hub](https://hub.docker.com/r/opswat/nginx-ingress)

  - For example:

    - latest image: opswat/nginx-ingress
    - or specify the tag: opswat/nginx-ingress:controller-5.4.1_ometascan-1.5.0_r1
- MD ICAP Server at least version v5.1.0, which has already enabled NGINX integration [NGINX Integration Configurations](/docs/mdicap/v5.14.1/configuration/enable-integration-with-nginx)

### [Pre-setup](/docs/mdicap/v5.14.1/integrations/ingress-solutions#pre-setup)

#### [Enable Nginx ingress on Minikube](/docs/mdicap/v5.14.1/integrations/ingress-solutions#enable-nginx-ingress-on-minikube)

- Start minikube

minikube start

- Install the NGINX Ingress controller, following this CLI

helm install <my-release> oci://ghcr.io/nginx/charts/nginx-ingress --version 2.5.2

- Verify that the NGINX Ingress controller is running

kubectl get ingressclasses

The output is similar to:

NAME CONTROLLER PARAMETERS AGE
nginx nginx.org/ingress-controller <none> 10m
#### [Change the default Nginx Ingress image to Nginx Ingress with the OMetascan module image](/docs/mdicap/v5.14.1/integrations/ingress-solutions#change-the-default-nginx-ingress-image-to-nginx-ingress-with-the-ometascan-module-image)

- Update the default image to opswat/nginx-ingress using the following command:

kubectl set image deployment/nginx-ingress-controller \
nginx-ingress=opswat/nginx-ingress

- Verify that the images have changed:

kubectl get deploy nginx-ingress-controller -o jsonpath='{.spec.template.spec.containers}'

The output:

[
{
"image": "opswat/nginx-ingress:controller-5.4.1_ometascan-1.5.0_r1",
"imagePullPolicy": "Always",
"name": "nginx-ingress",
}
]

- Verify that the NGINX Ingress controller is replaced and running

kubectl get pods -A | grep nginx-ingress

The output is similar to:

NAME READY STATUS RESTARTS AGE
nginx-ingress-controller-785746b95c-djcjx 1/1 Running 0 119s
#### [Enable OMetascan Module](/docs/mdicap/v5.14.1/integrations/ingress-solutions#enable-ometascan-module)

- Set **enable-ometascan: "true"** to turn on the OMetascan module on ConfigMaps of ingress-nginx-controller:

cat <<EOF | kubectl apply -f -
apiVersion: v1
data:
enable-ometascan: "true"
kind: ConfigMap
metadata:
annotations:
meta.helm.sh/release-name: nginx-ingress
meta.helm.sh/release-namespace: default
labels:
app.kubernetes.io/instance: nginx-ingress
app.kubernetes.io/managed-by: Helm
app.kubernetes.io/name: nginx-ingress
app.kubernetes.io/version: 5.4.1
helm.sh/chart: nginx-ingress-2.5.1
name: nginx-ingress
namespace: default
EOF
#### [Deploy Echo Server as Service A](/docs/mdicap/v5.14.1/integrations/ingress-solutions#deploy-echo-server-as-service-a)

refer to: <https://github.com/Ealenn/Echo-Server#kubernetes>

cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Namespace
metadata:
name: echoserver
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: echoserver
namespace: echoserver
spec:
replicas: 5
selector:
matchLabels:
app: echoserver
template:
metadata:
labels:
app: echoserver
spec:
containers:
- image: ealen/echo-server:latest
imagePullPolicy: IfNotPresent
name: echoserver
ports:
- containerPort: 80
env:
- name: PORT
value: "80"
---
apiVersion: v1
kind: Service
metadata:
name: echoserver
namespace: echoserver
spec:
ports:
- port: 80
targetPort: 80
protocol: TCP
type: ClusterIP
selector:
app: echoserver
EOF
#### [Example:](/docs/mdicap/v5.14.1/integrations/ingress-solutions#example)

- `/path1` rewrite to `/subpathA` (use ometascan)
- `/path2` rewrite to `/subpathB` (use ometascan)

  - Only PUT methods
  - Max client body size 100 Mb
- `/path3` rewrite to /`subpathC` (do not use ometascan)

cat <<EOF | kubectl apply -f -
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: ingress-rule-a
namespace: echoserver
annotations:
nginx.org/rewrite-target: /subpathA
nginx.org/ometascan-pass: "http://10.40.161.167:8043"
spec:
rules:
- host: testserver-a.com
http:
paths:
- path: /path1
pathType: Prefix
backend:
service:
name: echoserver
port:
number: 80
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: ingress-rule-b
namespace: echoserver
annotations:
nginx.org/rewrite-target: /subpathB
nginx.org/ometascan-pass: "http://10.40.161.167:8043"
nginx.org/ometascan-methods: "PUT"
nginx.org/client-max-body-size: 100M
spec:
rules:
- host: testserver-b.com
http:
paths:
- path: /path2
pathType: Prefix
backend:
service:
name: echoserver
port:
number: 80
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: ingress-rule-c
namespace: echoserver
annotations:
nginx.org/rewrite-target: /subpathC
spec:
rules:
- host: testserver-c.com
http:
paths:
- path: /path3
pathType: Prefix
backend:
service:
name: echoserver
port:
number: 80
EOF
## [OMetaScan NGINX Ingress on Kubernetes](/docs/mdicap/v5.14.1/integrations/ingress-solutions#ometascan-nginx-ingress-on-kubernetes)

### [Requirements](/docs/mdicap/v5.14.1/integrations/ingress-solutions#requirements)

- An existing K8S cluster
- Helm CLI
- NGINX Ingress with OMetascan module images:

# pull latest image
docker pull opswat/nginx-ingress
#or specific the tag
docker pull opswat/nginx-ingress:controller-5.4.1_ometascan-1.5.0_r1

- An existing MD ICAP Server on Kubernetes

### [Instructions](/docs/mdicap/v5.14.1/integrations/ingress-solutions#instructions)

Example:

#### [1. Install NGINX Ingress Controller via Helm Chart](/docs/mdicap/v5.14.1/integrations/ingress-solutions#1-install-nginx-ingress-controller-via-helm-chart)

helm install nginx-ingress oci://ghcr.io/nginx/charts/nginx-ingress \
--version 2.5.2

Output:

JavascriptCopyPulled: ghcr.io/nginx/charts/nginx-ingress:2.5.2
Digest: sha256:0d0548ec8f087ef431f2f7e26503775d99cd8f5644261f571d9133264d183094
NAME: nginx-ingress
LAST DEPLOYED: Wed May 20 15:07:07 2026
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
NGINX Ingress Controller 5.4.2 has been installed.
For release notes, see: https://docs.nginx.com/nginx-ingress-controller/changelog/
For Helm installation instructions, see: https://docs.nginx.com/nginx-ingress-controller/install/helm/

Verify the result, install nginx-ingress as CLI:

kubectl get pods -A | grep nginx-ingress

Output:

JavascriptCopyNAME READY STATUS RESTARTS AGE
nginx-ingress-controller-69fbfb9f44-frjgg 1/1 Running 0 69sInfo

Make sure your nginx install with status of the pod nginx-ingress is running!

#### [2. Replace The Ingress Controller Image](/docs/mdicap/v5.14.1/integrations/ingress-solutions#2-replace-the-ingress-controller-image)

To replace the ingress controller image, we need to patch the existing k8s resource (deployment, DaemonSet, etc.) for the existing ingress controller to include the new image. For this, edit the `ingress-controller-patch-image.yml` file and replace the container name to match the existing controller and run the following command (replace 'deployment' and 'ingress-nginx-controller' with your specific resource type and name for the controller):

`ingress-controller-patch-image.yml`

---
spec:
template:
spec:
containers:
- name: nginx-ingress
image: opswat/nginx-ingresskubectl patch deployment nginx-ingress-controller \
--patch-file ingress-controller-patch-image.yml

Output:

JavascriptCopydeployment.apps/nginx-ingress-controller patched

Create the file `update-configmap-ingress-controller.yml`

JavascriptCopyapiVersion: v1
kind: ConfigMap
metadata:
name: nginx-ingress
namespace: default
data:
enable-ometascan: "true"kubectl apply -f update-configmap-ingress-controller.yml

Output:

JavascriptCopyconfigmap/nginx-ingress configured
#### [3. Deploy A Service To Test with MetaDefender ICAP Server](/docs/mdicap/v5.14.1/integrations/ingress-solutions#3-deploy-a-service-to-test-with-metadefender-icap-server)

3.1. Create deployment sample:

kubectl create deployment backend --image=gcr.io/google-samples/hello-app:1.0

Output:

3.2.Expose service sample:

kubectl expose deployment backend --port=8080 --type=ClusterIP

Output:

3.3.Create file ingress for sample app:

`ingress-be.yml`

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: ingress-be-rule-a
annotations:
nginx.org/rewrite-target: /subpathA
nginx.org/ometascan-pass: "http://md-icapsrv:8043" # Replace with the address and port of an existing ICAP instace, for example, if ICAP is running in the same cluster: http://<ICAP_SERVICE_NAME>.<ICAP_NAMESPACE>.svc.cluster.local:<ICAP_PORT>
spec:
ingressClassName: nginx
rules:
- host: testserver-a.com
http:
paths:
- path: /subpathA
pathType: Prefix
backend:
service:
name: backend
port:
number: 8080
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: ingress-be-rule-b
annotations:
nginx.org/rewrite-target: /subpathB
nginx.org/ometascan-pass: "http://md-icapsrv:8043" # Replace with the address and port of an existing ICAP instace, for example, if ICAP is running in the same cluster: http://<ICAP_SERVICE_NAME>.<ICAP_NAMESPACE>.svc.cluster.local:<ICAP_PORT>
nginx.org/ometascan-methods: "PUT"
nginx.org/client-body-buffer-size: 100M
spec:
ingressClassName: nginx
rules:
- host: testserver-b.com
http:
paths:
- path: /subpathB
pathType: Prefix
backend:
service:
name: backend
port:
number: 8080
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: ingress-be-rule-c
annotations:
nginx.org/rewrite-target: /subpathC
spec:
ingressClassName: nginx
rules:
- host: testserver-c.com
http:
paths:
- path: /subpathC
pathType: Prefix
backend:
service:
name: backend
port:
number: 8080kubectl apply -f ingress-be.yml

Output:

Add the following line to the bottom of the `/etc/hosts` file on your computer (you will need administrator access):

10.40.162.150 testserver.com mdicapsrvs-ui.opswat.local
Send requests to Backend:
curl -X GET testserver-a.com/subPathA
curl -X POST testserver-a.com/subPathA
curl -X PUT testserver-b.com/subPathB
curl -X GET testserver-b.com/subPathB
curl -X GET testserver-c.com/subPathC

The expected MD ICAP Server will scan requests
