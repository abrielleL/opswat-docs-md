<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/enable-https -->

# Enable HTTPs

## [**Step 1 — Create TLS secret**](/docs/mdcluster/container-deployment/enable-https#step-1--create-tls-secret)

Create cert and key with x509 format and add TLS secret:

kubectl create secret tls mdcluster-control-center-tls \
--cert=<control-center-cert-file> --key=<control-center-key-file>
kubectl create secret tls mdcluster-api-gateway-tls \
--cert=<api-gateway-cert-file> --key=<api-gateway-key-file>
## [**Step 2 — Create TLS secret**](/docs/mdcluster/container-deployment/enable-https#step-2--create-tls-secret)

Update `override-values.yaml` in [Quick start](/docs/mdcluster/container-deployment/quick-start)

control-center:
tls:
enabled: true
secretName: mdcluster-control-center-tls
workers:
api-gateway:
tls:
enabled: true
secretName: mdcluster-api-gateway-tls
## [**Step 3 — Apply config**](/docs/mdcluster/container-deployment/enable-https#step-3--apply-config)

helm upgrade mdcluster ./mdcluster --install -f ./override-values.yaml
