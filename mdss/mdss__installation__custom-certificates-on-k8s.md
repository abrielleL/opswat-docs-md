<!-- source: https://www.opswat.com/docs/mdss/installation/custom-certificates-on-k8s -->

# Custom certificates on K8S

Custom certificates need to be loaded in MDSS when connecting to services that use a private TLS/SSL certificate like MD Core, storage units, external databases etc. These certificates need to be loaded into the K8S cluster as a secret which can be mounted into the appropriate services by adding the following section to the values file:

YamlCopymdss_components:
<SERVICE_NAME>:
update_ca: true
customMounts:
- mountPath: "/usr/local/share/ca-certificates/my-custom-cert.crt"
name: my-cert
subPath: cert-data
customVolumes:
- name: my-cert
secret:
secretName: my-custom-cert

An example values file where certificates are loaded into multiple MDSS services can be found on our GitHub repo here: <https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdss-custom-certs-example.yml>
