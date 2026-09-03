<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/container-deployment/licensing-in-k8s -->

# Licensing in K8S

## [Environment variable for containers](/docs/mdcore/v5.21.0/container-deployment/licensing-in-k8s#environment-variable-for-containers)

The container image will use the `LICENSE_KEY` environment variable to run the automation to activate and deactivate the container license.

## [Main Licensing Automation in K8S](/docs/mdcore/v5.21.0/container-deployment/licensing-in-k8s#main-licensing-automation-in-k8s)

Every time a pod of md-core is created it will create a deployment id attached to that pod so it is automatically activated. In case the pod goes down it will be automatically deactivated thanks to the logic included in the app container that will make a call to the OPSWAT Activation Server.

Following the best practices for Kubernetes, MetaDefender Core handles the SIGTERM signal, sent by a Kubernetes cluster component to the app container, and run the logic to deactivate the deployment id linked to the pod.

Warning

The md-core pods use the secrets **mdcore-license-key** to generate a deployment id and activate that pod. In case of failure on activation the app container will restart until that secret is properly set up with a license key with enough activations.

## [Licensing Clean Up on Involuntary Disruption (Optional)](/docs/mdcore/v5.21.0/container-deployment/licensing-in-k8s#licensing-clean-up-on-involuntary-disruption-optional)

Aiming to cover as much as possible situations of disruption when running MetaDefender Core application in Kubernetes, OPSWAT provides with a mechanism to cleanup the zombie activations in case an old app container terminated did not get the SIGTERM signal from the Kubernetes cluster.

### [How to enable licensing Clean Up](/docs/mdcore/v5.21.0/container-deployment/licensing-in-k8s#how-to-enable-licensing-clean-up)

When providing the environment variable `LICENSING_CLEANUP` in the MetaDefender Core pod, it will store licensing information in a the secret **mdcore-licensing** that will be created by the pod in case it is not already created. Therefore it is needed to create a role that will be bind to the default service account that the pod is using by namespace.

#### [Step by step using helm and kubectl](/docs/mdcore/v5.21.0/container-deployment/licensing-in-k8s#step-by-step-using-helm-and-kubectl)

- Set Up environment variables

  - variables already in the latest helm chart version. Only needed to change the flag to "true"

Values.ymlCopyenv:
LICENSING_CLEANUP: true
## ADD to the rest of the environment variables
md-core:
env:
- name: MY_POD_NAME
valueFrom:
fieldRef:
fieldPath: metadata.name
- name: MY_POD_NAMESPACE
valueFrom:
fieldRef:
fieldPath: metadata.namespace
extra_labels:
name: md-core

- Modify `core-worker-role.yml` and `core-worker-role-binding.yml` changing the namespace if needed
- Create **Role** and **RoleBinding** with the following commands

BashCopy# from root path of github metadefender-k8s project
kubectl apply -f example_scripts/core-worker-role.yml
kubectl apply -f example_scripts/core-worker-role-binding.yml
