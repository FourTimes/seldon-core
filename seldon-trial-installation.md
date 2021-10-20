seldon trial installtion steps

sudo apt install apache2-utils
mkdir -p ${HOME}/.config/seldon/seldon-deploy/
vim ${HOME}/.config/seldon/seldon-deploy/sdconfig.txt

```txt

GIT_USER="xxxxxx"
GIT_TOKEN="xxxxxx"
GIT_EMAIL="jjino@xxxx.com"
ENABLE_GIT_SSH_CREDS=false
SD_USER_EMAIL="admin@seldon-ey.io"
SD_PASSWORD="ChangeMe@123"
EXTERNAL_HOST=                             # This can be blank
EXTERNAL_PROTOCOL=http                    # "https" or "http"
KFSERVING_PROTOCOL=$EXTERNAL_PROTOCOL
MULTITENANT=false                         # Restricts permissions to namespace-level. Ask seldon before using.
ENABLE_APP_AUTH=true                      # 'true' or 'false'
VIRTUALSERVICE_CREATE=true
ENABLE_METADATA_POSTGRES=true             # If false will skip installing PostgreSQL in the trial cluster and metadata API will be unavailable.
ENABLE_OPA=false                          # If true will fetch OPA policies from a `seldon-deploy-policies` config map from the namespace Deploy is running in.
ENABLE_PROJECT_BASED_AUTH=false           # If true will authorize requests to resources based on what access does the user have to all models in that resource.
ENABLE_AUDIT=true                         # If true will setup a fluentd instance to forward Deploy's audit logs to a minio bucket.

```
 Use the following script to check or create an initial file to fill in.

```bash
# Default Trial Installation¶

TAG=1.4.0 && \
    docker create --name=tmp-sd-container seldonio/seldon-deploy-server:$TAG && \
    docker cp tmp-sd-container:/seldon-deploy-dist/seldon-deploy-install.tar.gz . && \
    docker rm -v tmp-sd-container

tar -xzf seldon-deploy-install.tar.gz


cd seldon-deploy-install
./check-config
./prerequisites-setup/default-setup.sh
./sd-setup/sd-install-default






```




installation process



```txt

[sepoy@xps seldon-deploy-install]$ ./prerequisites-setup/default-setup.sh
+++ dirname ./prerequisites-setup/default-setup.sh
++ cd ./prerequisites-setup
++ pwd
+ STARTUP_DIR=/home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ SELDON_CORE_DIR=
+ KFSERVING_DIR=
+ SELDON_CORE_VERSION=v1.9.1
+ KFSERVING_TAG=v0.4.1
+ ENABLE_KNATIVE_XIP=true
+ TEMPRESOURCES=/tmp/tempresources
+ SDCONFIG_FILE=/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
+ source /home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
++ GIT_USER=fourtimes
++ GIT_TOKEN=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
++ GIT_EMAIL=jjino@protonmail.com
++ ENABLE_GIT_SSH_CREDS=false
++ SD_USER_EMAIL=admin@seldon-ey.io
++ SD_PASSWORD=ChangeMe@123
++ XTERNAL_HOST=
++ EXTERNAL_PROTOCOL=http
++ KFSERVING_PROTOCOL=http
++ MULTITENANT=false
++ ENABLE_APP_AUTH=true
++ VIRTUALSERVICE_CREATE=true
++ ENABLE_METADATA_POSTGRES=true
++ ENABLE_OPA=false
++ ENABLE_PROJECT_BASED_AUTH=false
++ ENABLE_AUDIT=true
+ ENABLE_METADATA_POSTGRES=true
+ check_creds
+ ((  18 < 8  ))
+ ((  12 < 8  ))
+ setup_tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/clean
removed /tmp/tempresources
+ mkdir -p /tmp/tempresources
+ create_istio
+ cd /tmp/tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/istio/install_istio_new.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   102  100   102    0     0     70      0  0:00:01  0:00:01 --:--:--    70
100  4549  100  4549    0     0   2086      0  0:00:02  0:00:02 --:--:--     0

Downloading istio-1.7.3 from https://github.com/istio/istio/releases/download/1.7.3/istio-1.7.3-linux-amd64.tar.gz ...

Istio 1.7.3 Download Complete!

Istio has been successfully downloaded into the istio-1.7.3 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /tmp/tempresources/istio-1.7.3/bin directory to your environment path variable with:
	 export PATH="$PATH:/tmp/tempresources/istio-1.7.3/bin"

Begin the Istio pre-installation check by running:
	 istioctl x precheck 

Need more information? Visit https://istio.io/latest/docs/setup/install/ 
Installing istio
✔ Istio core installed                                                                                                                                                                        
✔ Istiod installed                                                                                                                                                                            
✔ Addons installed                                                                                                                                                                            
✔ Ingress gateways installed                                                                                                                                                                  
✔ Installation complete                                                                                                                                                                       istio & gateway setup completed
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ wait_istio_ready
+ kubectl rollout status -n istio-system deployment.v1.apps/istio-ingressgateway
deployment "istio-ingressgateway" successfully rolled out
+ configure_https
+ '[' http = https ']'
+ create_knative
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/knative
+ ./install_knative.sh
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev created
namespace/knative-serving created
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-serving-core created
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding created
serviceaccount/controller created
clusterrole.rbac.authorization.k8s.io/knative-serving-admin created
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy created
configmap/config-autoscaler created
configmap/config-defaults created
configmap/config-deployment created
configmap/config-domain created
configmap/config-features created
configmap/config-gc created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-network created
configmap/config-observability created
configmap/config-tracing created
horizontalpodautoscaler.autoscaling/activator created
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb created
deployment.apps/activator created
service/activator-service created
deployment.apps/autoscaler created
service/autoscaler created
deployment.apps/controller created
service/controller created
deployment.apps/webhook created
service/webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev created
secret/webhook-certs created
clusterrole.rbac.authorization.k8s.io/knative-serving-istio created
gateway.networking.istio.io/knative-ingress-gateway created
gateway.networking.istio.io/cluster-local-gateway created
gateway.networking.istio.io/knative-local-gateway created
service/knative-local-gateway created
peerauthentication.security.istio.io/webhook created
peerauthentication.security.istio.io/istio-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev created
secret/istio-webhook-certs created
configmap/config-istio created
deployment.apps/networking-istio created
deployment.apps/istio-webhook created
service/istio-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev created
namespace/knative-eventing created
serviceaccount/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator created
serviceaccount/pingsource-mt-adapter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
serviceaccount/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding created
configmap/config-br-default-channel created
configmap/config-br-defaults created
configmap/default-ch-webhook created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-observability created
configmap/config-tracing created
deployment.apps/eventing-controller created
deployment.apps/pingsource-mt-adapter created
deployment.apps/eventing-webhook created
service/eventing-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver created
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter created
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress created
clusterrole.rbac.authorization.k8s.io/eventing-config-reader created
clusterrole.rbac.authorization.k8s.io/channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
clusterrole.rbac.authorization.k8s.io/podspecable-binding created
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding created
clusterrole.rbac.authorization.k8s.io/source-observer created
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer created
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev created
secret/eventing-webhook-certs created
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev created
Sleep and run again - needed for Kind install as not all CRDs get installed sometimes
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
namespace/knative-serving unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-core unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding unchanged
serviceaccount/controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-admin configured
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy unchanged
configmap/config-autoscaler unchanged
configmap/config-defaults unchanged
configmap/config-deployment unchanged
configmap/config-domain unchanged
configmap/config-features unchanged
configmap/config-gc unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-network unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
horizontalpodautoscaler.autoscaling/activator unchanged
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb configured
deployment.apps/activator configured
service/activator-service unchanged
deployment.apps/autoscaler unchanged
service/autoscaler unchanged
deployment.apps/controller configured
service/controller unchanged
deployment.apps/webhook unchanged
service/webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev unchanged
secret/webhook-certs unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-istio unchanged
gateway.networking.istio.io/knative-ingress-gateway unchanged
gateway.networking.istio.io/cluster-local-gateway unchanged
gateway.networking.istio.io/knative-local-gateway unchanged
service/knative-local-gateway unchanged
peerauthentication.security.istio.io/webhook unchanged
peerauthentication.security.istio.io/istio-webhook unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev unchanged
secret/istio-webhook-certs unchanged
configmap/config-istio unchanged
deployment.apps/networking-istio unchanged
deployment.apps/istio-webhook unchanged
service/istio-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
namespace/knative-eventing unchanged
serviceaccount/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator unchanged
serviceaccount/pingsource-mt-adapter unchanged
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
serviceaccount/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding unchanged
configmap/config-br-default-channel unchanged
configmap/config-br-defaults unchanged
configmap/default-ch-webhook unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
deployment.apps/eventing-controller unchanged
deployment.apps/pingsource-mt-adapter configured
deployment.apps/eventing-webhook unchanged
service/eventing-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver configured
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress unchanged
clusterrole.rbac.authorization.k8s.io/eventing-config-reader unchanged
clusterrole.rbac.authorization.k8s.io/channelable-manipulator configured
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
clusterrole.rbac.authorization.k8s.io/podspecable-binding configured
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding unchanged
clusterrole.rbac.authorization.k8s.io/source-observer configured
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev unchanged
secret/eventing-webhook-certs unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev unchanged
deployment "eventing-controller" successfully rolled out
service/autoscaler annotated
service/autoscaler annotated
service/activator-service annotated
service/activator-service annotated
deployment "eventing-controller" successfully rolled out
deployment "eventing-webhook" successfully rolled out
configmap/config-imc-event-dispatcher created
clusterrole.rbac.authorization.k8s.io/imc-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/imc-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/imc-controller created
serviceaccount/imc-controller created
clusterrole.rbac.authorization.k8s.io/imc-dispatcher created
service/imc-dispatcher created
serviceaccount/imc-dispatcher created
clusterrolebinding.rbac.authorization.k8s.io/imc-controller created
clusterrolebinding.rbac.authorization.k8s.io/imc-dispatcher created
customresourcedefinition.apiextensions.k8s.io/inmemorychannels.messaging.knative.dev created
deployment.apps/imc-controller created
deployment.apps/imc-dispatcher created
deployment "imc-controller" successfully rolled out
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-channel-broker-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
serviceaccount/mt-broker-filter created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
serviceaccount/mt-broker-ingress created
clusterrolebinding.rbac.authorization.k8s.io/eventing-mt-channel-broker-controller created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
deployment.apps/mt-broker-filter created
service/broker-filter created
deployment.apps/mt-broker-ingress created
service/broker-ingress created
deployment.apps/mt-broker-controller created
horizontalpodautoscaler.autoscaling/broker-ingress-hpa created
horizontalpodautoscaler.autoscaling/broker-filter-hpa created
deployment "mt-broker-controller" successfully rolled out
deployment "mt-broker-filter" successfully rolled out
+ '[' true = true ']'
+ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.18.0/serving-default-domain.yaml
job.batch/default-domain created
service/default-domain-service created
+ install_argo
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/argo
+ ./argo.sh
namespace/argo created
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/clusterworkflowtemplates.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/cronworkflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workfloweventbindings.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflowtemplates.argoproj.io created
serviceaccount/argo created
serviceaccount/argo-server created
role.rbac.authorization.k8s.io/argo-role created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-admin created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-edit created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-view created
clusterrole.rbac.authorization.k8s.io/argo-cluster-role created
clusterrole.rbac.authorization.k8s.io/argo-server-cluster-role created
rolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-server-binding created
configmap/workflow-controller-configmap created
service/argo-server created
service/workflow-controller-metrics created
deployment.apps/argo-server created
deployment.apps/workflow-controller created
configmap/workflow-controller-configmap configured
+ install_minio
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/minio
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./minio.sh
TEMPRESOURCES IS /tmp/tempresources
SD_USER_EMAIL IS admin@seldon-ey.io
namespace/minio-system created
"minio" has been added to your repositories
Release "minio" does not exist. Installing it now.
NAME: minio
LAST DEPLOYED: Wed Oct 20 12:13:45 2021
NAMESPACE: minio-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Minio can be accessed via port 9000 on the following DNS name from within your cluster:
minio.minio-system.svc.cluster.local

To access Minio from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace minio-system -l "release=minio" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace minio-system

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access Minio server on http://localhost:9000. Follow the below steps to connect to Minio server with mc client:

  1. Download the Minio mc client - https://docs.minio.io/docs/minio-client-quickstart-guide

  2. Get the ACCESS_KEY=$(kubectl get secret minio -o jsonpath="{.data.accesskey}" | base64 --decode) and the SECRET_KEY=$(kubectl get secret minio -o jsonpath="{.data.secretkey}" | base64 --decode)

  3. mc alias set minio-local http://localhost:9000 "$ACCESS_KEY" "$SECRET_KEY" --api s3v4

  4. mc ls minio-local

Alternately, you can use your browser or the Minio SDK to access the server - https://docs.minio.io/categories/17
virtualservice.networking.istio.io/minio created
+ install_EFK_and_logger
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk
+ export TEMPRESOURCES
+ ./install_efk.sh
TEMPRESOURCES IS /tmp/tempresources
Error from server (AlreadyExists): namespaces "seldon-logs" already exists
namespace seldon-logs exists
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/elastic-credentials created
secret/elastic-credentials created
Cloning into 'opendistro-build'...
remote: Enumerating objects: 7421, done.
remote: Counting objects: 100% (531/531), done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 7421 (delta 343), reused 422 (delta 266), pack-reused 6890
Receiving objects: 100% (7421/7421), 1.90 MiB | 805.00 KiB/s, done.
Resolving deltas: 100% (5084/5084), done.
Fetching origin
Note: switching to 'tags/v1.13.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at aabb00f Modify script and workflow for AMI to include ARM64  (#738)
Successfully packaged chart and saved it to: /tmp/tempresources/opendistro-build/helm/opendistro-es/opendistro-es-1.13.2.tgz
Release "elasticsearch" does not exist. Installing it now.
W1020 12:14:37.341245   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:43.646754   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:44.920126   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:57.940282   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:59.050377   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:59.050983   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
NAME: elasticsearch
LAST DEPLOYED: Wed Oct 20 12:14:34 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
Release "fluentd" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: fluentd
LAST DEPLOYED: Wed Oct 20 12:15:10 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=seldon-logs get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.
Waiting for deployment "elasticsearch-opendistro-es-kibana" rollout to finish: 0 of 1 updated replicas are available...
deployment "elasticsearch-opendistro-es-kibana" successfully rolled out
+ ./eventing_for_logs_ns.sh
broker.eventing.knative.dev/default created
knative broker created
+ kubectl apply -f /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk/kibana-virtualservice.yaml
virtualservice.networking.istio.io/kibana created
+ install_seldon_core
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/seldon-core
+ export TEMPRESOURCES
+ export SELDON_CORE_VERSION
+ export MULTITENANT
+ export EXTERNAL_PROTOCOL
+ ./install_seldon_core.sh
SELDON CORE VERSION v1.9.1
Cloning into 'seldon-core'...
remote: Enumerating objects: 130545, done.
remote: Counting objects: 100% (2898/2898), done.
remote: Compressing objects: 100% (1172/1172), done.
remote: Total 130545 (delta 1846), reused 2511 (delta 1606), pack-reused 127647
Receiving objects: 100% (130545/130545), 212.37 MiB | 824.00 KiB/s, done.
Resolving deltas: 100% (78770/78770), done.
Note: switching to '8ad2ede5ca18e321f8603f1e2a821e767af000de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

using /tmp/tempresources/seldon-core
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
gateway.networking.istio.io/seldon-gateway configured
Release "seldon-core" does not exist. Installing it now.
W1020 12:21:32.726503   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
W1020 12:21:57.693208   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
NAME: seldon-core
LAST DEPLOYED: Wed Oct 20 12:21:13 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
Waiting for deployment "seldon-controller-manager" rollout to finish: 0 of 1 updated replicas are available...
deployment "seldon-controller-manager" successfully rolled out
+ install_analytics
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/prometheus
+ export TEMPRESOURCES
+ ./seldon-core-analytics.sh
configmap/model-usage-rules created
Error from server (NotFound): deployments.apps "seldon-core-analytics-prometheus-seldon" not found
Release "seldon-core-analytics" does not exist. Installing it now.
W1020 12:28:18.796115   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:20.023979   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:49.096327   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:50.323697   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:51.355141   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:52.574403   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:53.599335   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:55.648768   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:56.670352   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:57.676505   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:58.922424   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:00.149772   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:01.379295   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:03.834611   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
W1020 12:29:22.466916   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:22.467337   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:25.947779   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.951773   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.988757   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.994807   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.995223   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:26.358782   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358910   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359018   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358798   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359349   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.767071   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:27.176581   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
NAME: seldon-core-analytics
LAST DEPLOYED: Wed Oct 20 12:28:15 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
+ install_kfserving
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/kfserving
+ export TEMPRESOURCES
+ export KFSERVING_TAG
+ ./install_kfserving.sh
TEMPRESOURCES IS /tmp/tempresources
KFSERVING_TAG v0.4.1
Cloning into 'kfserving'...
remote: Enumerating objects: 44567, done.
remote: Counting objects: 100% (1826/1826), done.
remote: Compressing objects: 100% (1192/1192), done.
remote: Total 44567 (delta 839), reused 1249 (delta 566), pack-reused 42741
Receiving objects: 100% (44567/44567), 116.21 MiB | 800.00 KiB/s, done.
Resolving deltas: 100% (17763/17763), done.
Note: switching to 'f253dd529ba25c080ca458d8dc36fd0a19bbd473'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f253dd52 update 0.4.1 yaml (#1176)
using /tmp/tempresources/kfserving
namespace/kfserving-system created
Warning: resource namespaces/kfserving-system is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/kfserving-system configured
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/inferenceservices.serving.kubeflow.org created
Warning: admissionregistration.k8s.io/v1beta1 MutatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 MutatingWebhookConfiguration
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
role.rbac.authorization.k8s.io/leader-election-role created
clusterrole.rbac.authorization.k8s.io/kfserving-manager-role created
clusterrole.rbac.authorization.k8s.io/kfserving-proxy-role created
rolebinding.rbac.authorization.k8s.io/leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-proxy-rolebinding created
configmap/inferenceservice-config created
secret/kfserving-webhook-server-secret created
service/kfserving-controller-manager-metrics-service created
service/kfserving-controller-manager-service created
service/kfserving-webhook-server-service created
statefulset.apps/kfserving-controller-manager created
Warning: admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Certificate" in version "cert-manager.io/v1alpha2"
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Issuer" in version "cert-manager.io/v1alpha2"
configmap/inferenceservice-config patched
service: kfserving-webhook-server-service
namespace: kfserving-system
secret: kfserving-webhook-server-cert
webhookDeploymentName: kfserving-controller-manager-0
webhookConfigName: inferenceservice.serving.kubeflow.org
creating certs in tmpdir /tmp/tmp.VFjc8KH97E 
Generating RSA private key, 2048 bit long modulus (2 primes)
.......................+++++
...........................................................+++++
e is 65537 (0x010001)
Generating RSA private key, 2048 bit long modulus (2 primes)
........................................................................................+++++
......................................................................+++++
e is 65537 (0x010001)
Signature ok
subject=CN = kfserving-webhook-server-service.kfserving-system.svc
Getting CA Private Key
W1020 12:32:50.683819   37974 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
secret/kfserving-webhook-server-cert created
pod "kfserving-controller-manager-0" deleted
webhook kfserving-controller-manager-0 is restarted to utilize the new secret
CA Certificate:
-----BEGIN CERTIFICATE-----
MIIDYTCCAkmgAwIBAgIUIwKbuXlVEBkLnIHYAy0VIOtbhEIwDQYJKoZIhvcNAQEL
BQAwQDE+MDwGA1UEAww1a2ZzZXJ2aW5nLXdlYmhvb2stc2VydmVyLXNlcnZpY2Uu
a2ZzZXJ2aW5nLXN5c3RlbS5zdmMwHhcNMjExMDIwMDcwMjUwWhcNMjIxMDIwMDcw
MjUwWjBAMT4wPAYDVQQDDDVrZnNlcnZpbmctd2ViaG9vay1zZXJ2ZXItc2Vydmlj
ZS5rZnNlcnZpbmctc3lzdGVtLnN2YzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKqYeLIbze8FaJMmaThqsu9gfXsBwXubosNWODeP9KkN1K0MZhPQc2uJ
5fSwW13cxRaXYnOfaT2AmYdXJZKLBKSWCPPli2rIG9sK0uSm6uR6F/wiXRxlhWHI
R2IXzvbChEczanKCj9WGqolBv2pORYToROmtKxrOmgIx80bwWMKRYARskZtXwUe2
q1OYIsjM0iTMxLgTb1sQs1fXXQ2IgGgYXsonK7FRkcfI7mN0BmcOesOnTw1FAcPO
I7D+FKVZfiQxTY8ktx7WxlszKcmh7hd0KOJC2sHfCUJf82O4h8R/ugtSeS/m1K+n
171KW4DpYccvbKDLA8KotO7nTaN5YXcCAwEAAaNTMFEwHQYDVR0OBBYEFNhFaXMQ
qRjegiNmObr9mZHh4QdtMB8GA1UdIwQYMBaAFNhFaXMQqRjegiNmObr9mZHh4Qdt
MA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAA2wU0Ei06Mrd8hW
yscVL1R0odDF5m2pAVhE2Jgig3Di2gLNaEHT0jjOVSWoDRDyxPy8I0a+KirqlWwA
5/2uQiAE60rTLugKO+xdHgkGp3j/QWK6bczlm4S2b5cD0blv+u0TFbnikbKUFRJ1
EpBuLcKWQJUOEvmgtikYeDEsyLrozu8OnxHXiO1bn2ZRPhnDHvbgNb+IeBaeq+a9
NFoN87NOiqXVTxLUt7W4JhazM8ZuOeEfQUzl7k3Wgle9aY37rviD14MMboPigA74
5OB8HTMrpvcCvvqJaszuxirSwHK+y54rKbuNiHQGbnC384viA/JY9qGD4R1kopu0
W+A9NeU=
-----END CERTIFICATE-----
Encoded CA:
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURZVENDQWttZ0F3SUJBZ0lVSXdLYnVYbFZFQmtMbklIWUF5MFZJT3RiaEVJd0RRWUpLb1pJaHZjTkFRRUwKQlFBd1FERStNRHdHQTFVRUF3dzFhMlp6WlhKMmFXNW5MWGRsWW1odmIyc3RjMlZ5ZG1WeUxYTmxjblpwWTJVdQphMlp6WlhKMmFXNW5MWE41YzNSbGJTNXpkbU13SGhjTk1qRXhNREl3TURjd01qVXdXaGNOTWpJeE1ESXdNRGN3Ck1qVXdXakJBTVQ0d1BBWURWUVFERERWclpuTmxjblpwYm1jdGQyVmlhRzl2YXkxelpYSjJaWEl0YzJWeWRtbGoKWlM1clpuTmxjblpwYm1jdGMzbHpkR1Z0TG5OMll6Q0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQwpBUW9DZ2dFQkFLcVllTEliemU4RmFKTW1hVGhxc3U5Z2ZYc0J3WHVib3NOV09EZVA5S2tOMUswTVpoUFFjMnVKCjVmU3dXMTNjeFJhWFluT2ZhVDJBbVlkWEpaS0xCS1NXQ1BQbGkycklHOXNLMHVTbTZ1UjZGL3dpWFJ4bGhXSEkKUjJJWHp2YkNoRWN6YW5LQ2o5V0dxb2xCdjJwT1JZVG9ST210S3hyT21nSXg4MGJ3V01LUllBUnNrWnRYd1VlMgpxMU9ZSXNqTTBpVE14TGdUYjFzUXMxZlhYUTJJZ0dnWVhzb25LN0ZSa2NmSTdtTjBCbWNPZXNPblR3MUZBY1BPCkk3RCtGS1ZaZmlReFRZOGt0eDdXeGxzektjbWg3aGQwS09KQzJzSGZDVUpmODJPNGg4Ui91Z3RTZVMvbTFLK24KMTcxS1c0RHBZY2N2YktETEE4S290TzduVGFONVlYY0NBd0VBQWFOVE1GRXdIUVlEVlIwT0JCWUVGTmhGYVhNUQpxUmplZ2lObU9icjltWkhoNFFkdE1COEdBMVVkSXdRWU1CYUFGTmhGYVhNUXFSamVnaU5tT2JyOW1aSGg0UWR0Ck1BOEdBMVVkRXdFQi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBMndVMEVpMDZNcmQ4aFcKeXNjVkwxUjBvZERGNW0ycEFWaEUySmdpZzNEaTJnTE5hRUhUMGpqT1ZTV29EUkR5eFB5OEkwYStLaXJxbFd3QQo1LzJ1UWlBRTYwclRMdWdLTyt4ZEhna0dwM2ovUVdLNmJjemxtNFMyYjVjRDBibHYrdTBURmJuaWtiS1VGUkoxCkVwQnVMY0tXUUpVT0V2bWd0aWtZZURFc3lMcm96dThPbnhIWGlPMWJuMlpSUGhuREh2YmdOYitJZUJhZXErYTkKTkZvTjg3Tk9pcVhWVHhMVXQ3VzRKaGF6TThadU9lRWZRVXpsN2szV2dsZTlhWTM3cnZpRDE0TU1ib1BpZ0E3NAo1T0I4SFRNcnB2Y0N2dnFKYXN6dXhpclN3SEsreTU0cktidU5pSFFHYm5DMzg0dmlBL0pZOXFHRDRSMWtvcHUwClcrQTlOZVU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K 

patching ca bundle for mutating webhook configuration...
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
patching ca bundle for validating webhook configuration...
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
+ configure_namespaces
+ kubectl create namespace seldon
namespace/seldon created
+ kubectl label ns seldon seldon.restricted=false --overwrite=true
namespace/seldon labeled
+ kubectl label ns seldon serving.kubeflow.org/inferenceservice=enabled --overwrite=true
namespace/seldon labeled
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/configure-batch-on-ns
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./batch-sa-for-ns.sh
TEMPRESOURCES IS /tmp/tempresources
role.rbac.authorization.k8s.io/workflow created
serviceaccount/workflow created
rolebinding.rbac.authorization.k8s.io/workflow created
secret/seldon-job-secret created
Error from server (NotFound): namespaces "kubeflow" not found
secret/seldon-job-secret configured
configured for minio in minio-system
+ install_postgres
+ '[' true = true ']'
+ echo 'Installing postgres...'
Installing postgres...
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/postgres
+ export TEMPRESOURCES
+ export STARTUP_DIR
+ POSTGRES_MANIFEST=minimal-postgres-manifest.yaml
+ ./install_postgres.sh
Installing zalando postgres operator and a db instance if required
Cloning into 'postgres-operator'...
remote: Enumerating objects: 22250, done.
remote: Counting objects: 100% (2142/2142), done.
remote: Compressing objects: 100% (964/964), done.
remote: Total 22250 (delta 1504), reused 1700 (delta 1145), pack-reused 20108
Receiving objects: 100% (22250/22250), 8.71 MiB | 915.00 KiB/s, done.
Resolving deltas: 100% (15803/15803), done.
Note: switching to 'v1.6.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c18241f1 Bump v1.6.2 (#1433)
namespace/postgres created
Release "postgres-operator" does not exist. Installing it now.
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: postgres-operator
LAST DEPLOYED: Wed Oct 20 12:34:07 2021
NAMESPACE: postgres
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that postgres-operator has started, run:

  kubectl --namespace=postgres get pods -l "app.kubernetes.io/name=postgres-operator"
postgresql.acid.zalan.do/seldon-metadata-storage created
The postgres secret has been created by the operator...
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/metadata-postgres created
+ install_keycloak_auth
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/keycloak
+ ./install_keycloak.sh
Error from server (AlreadyExists): namespaces "seldon-system" already exists
secret/realm-secret created
Release "keycloak" does not exist. Installing it now.
NAME: keycloak
LAST DEPLOYED: Wed Oct 20 12:35:16 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
NOTES:
Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  keycloak-http.seldon-system.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

  export POD_NAME=$(kubectl get pods --namespace seldon-system -l app.kubernetes.io/instance=keycloak -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use Keycloak"
  kubectl port-forward --namespace seldon-system $POD_NAME 8080

Login with the following credentials:
Username: "admin@seldon-ey.io"

To retrieve the initial user password run:
kubectl get secret --namespace seldon-system keycloak-http -o jsonpath="{.data.password}" | base64 --decode; echo
virtualservice.networking.istio.io/keycloak created
Waiting for 1 pods to be ready...
statefulset rolling update complete 1 pods at revision keycloak-5d9666fb66...
Creating default keycloak user
 * Default user created
Creating API auth client
 * API client created
 * Keycloak setup completed
[sepoy@xps seldon-deploy-install]$ ./sd-setup/sd-install-default
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/git-creds configured
namespace/argocd configured
Error from server (AlreadyExists): namespaces "seldon-system" already exists
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/request-logger-auth configured
./sd-setup/sd-install-default: line 80: EXTERNAL_HOST: unbound variable
[sepoy@xps seldon-deploy-install]$ ./sd-setup/show-seldon-deploy-url
http://a38fbee579f06403bb22116c69dcb22d-972759690.us-east-2.elb.amazonaws.com/seldon-deploy/

```[sepoy@xps seldon-deploy-install]$ ./prerequisites-setup/default-setup.sh
+++ dirname ./prerequisites-setup/default-setup.sh
++ cd ./prerequisites-setup
++ pwd
+ STARTUP_DIR=/home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ SELDON_CORE_DIR=
+ KFSERVING_DIR=
+ SELDON_CORE_VERSION=v1.9.1
+ KFSERVING_TAG=v0.4.1
+ ENABLE_KNATIVE_XIP=true
+ TEMPRESOURCES=/tmp/tempresources
+ SDCONFIG_FILE=/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
+ source /home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
++ GIT_USER=fourtimes
++ GIT_TOKEN=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
++ GIT_EMAIL=jjino@protonmail.com
++ ENABLE_GIT_SSH_CREDS=false
++ SD_USER_EMAIL=admin@seldon-ey.io
++ SD_PASSWORD=ChangeMe@123
++ XTERNAL_HOST=
++ EXTERNAL_PROTOCOL=http
++ KFSERVING_PROTOCOL=http
++ MULTITENANT=false
++ ENABLE_APP_AUTH=true
++ VIRTUALSERVICE_CREATE=true
++ ENABLE_METADATA_POSTGRES=true
++ ENABLE_OPA=false
++ ENABLE_PROJECT_BASED_AUTH=false
++ ENABLE_AUDIT=true
+ ENABLE_METADATA_POSTGRES=true
+ check_creds
+ ((  18 < 8  ))
+ ((  12 < 8  ))
+ setup_tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/clean
removed /tmp/tempresources
+ mkdir -p /tmp/tempresources
+ create_istio
+ cd /tmp/tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/istio/install_istio_new.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   102  100   102    0     0     70      0  0:00:01  0:00:01 --:--:--    70
100  4549  100  4549    0     0   2086      0  0:00:02  0:00:02 --:--:--     0

Downloading istio-1.7.3 from https://github.com/istio/istio/releases/download/1.7.3/istio-1.7.3-linux-amd64.tar.gz ...

Istio 1.7.3 Download Complete!

Istio has been successfully downloaded into the istio-1.7.3 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /tmp/tempresources/istio-1.7.3/bin directory to your environment path variable with:
	 export PATH="$PATH:/tmp/tempresources/istio-1.7.3/bin"

Begin the Istio pre-installation check by running:
	 istioctl x precheck 

Need more information? Visit https://istio.io/latest/docs/setup/install/ 
Installing istio
✔ Istio core installed                                                                                                                                                                        
✔ Istiod installed                                                                                                                                                                            
✔ Addons installed                                                                                                                                                                            
✔ Ingress gateways installed                                                                                                                                                                  
✔ Installation complete                                                                                                                                                                       istio & gateway setup completed
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ wait_istio_ready
+ kubectl rollout status -n istio-system deployment.v1.apps/istio-ingressgateway
deployment "istio-ingressgateway" successfully rolled out
+ configure_https
+ '[' http = https ']'
+ create_knative
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/knative
+ ./install_knative.sh
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev created
namespace/knative-serving created
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-serving-core created
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding created
serviceaccount/controller created
clusterrole.rbac.authorization.k8s.io/knative-serving-admin created
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy created
configmap/config-autoscaler created
configmap/config-defaults created
configmap/config-deployment created
configmap/config-domain created
configmap/config-features created
configmap/config-gc created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-network created
configmap/config-observability created
configmap/config-tracing created
horizontalpodautoscaler.autoscaling/activator created
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb created
deployment.apps/activator created
service/activator-service created
deployment.apps/autoscaler created
service/autoscaler created
deployment.apps/controller created
service/controller created
deployment.apps/webhook created
service/webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev created
secret/webhook-certs created
clusterrole.rbac.authorization.k8s.io/knative-serving-istio created
gateway.networking.istio.io/knative-ingress-gateway created
gateway.networking.istio.io/cluster-local-gateway created
gateway.networking.istio.io/knative-local-gateway created
service/knative-local-gateway created
peerauthentication.security.istio.io/webhook created
peerauthentication.security.istio.io/istio-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev created
secret/istio-webhook-certs created
configmap/config-istio created
deployment.apps/networking-istio created
deployment.apps/istio-webhook created
service/istio-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev created
namespace/knative-eventing created
serviceaccount/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator created
serviceaccount/pingsource-mt-adapter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
serviceaccount/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding created
configmap/config-br-default-channel created
configmap/config-br-defaults created
configmap/default-ch-webhook created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-observability created
configmap/config-tracing created
deployment.apps/eventing-controller created
deployment.apps/pingsource-mt-adapter created
deployment.apps/eventing-webhook created
service/eventing-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver created
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter created
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress created
clusterrole.rbac.authorization.k8s.io/eventing-config-reader created
clusterrole.rbac.authorization.k8s.io/channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
clusterrole.rbac.authorization.k8s.io/podspecable-binding created
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding created
clusterrole.rbac.authorization.k8s.io/source-observer created
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer created
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev created
secret/eventing-webhook-certs created
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev created
Sleep and run again - needed for Kind install as not all CRDs get installed sometimes
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
namespace/knative-serving unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-core unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding unchanged
serviceaccount/controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-admin configured
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy unchanged
configmap/config-autoscaler unchanged
configmap/config-defaults unchanged
configmap/config-deployment unchanged
configmap/config-domain unchanged
configmap/config-features unchanged
configmap/config-gc unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-network unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
horizontalpodautoscaler.autoscaling/activator unchanged
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb configured
deployment.apps/activator configured
service/activator-service unchanged
deployment.apps/autoscaler unchanged
service/autoscaler unchanged
deployment.apps/controller configured
service/controller unchanged
deployment.apps/webhook unchanged
service/webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev unchanged
secret/webhook-certs unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-istio unchanged
gateway.networking.istio.io/knative-ingress-gateway unchanged
gateway.networking.istio.io/cluster-local-gateway unchanged
gateway.networking.istio.io/knative-local-gateway unchanged
service/knative-local-gateway unchanged
peerauthentication.security.istio.io/webhook unchanged
peerauthentication.security.istio.io/istio-webhook unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev unchanged
secret/istio-webhook-certs unchanged
configmap/config-istio unchanged
deployment.apps/networking-istio unchanged
deployment.apps/istio-webhook unchanged
service/istio-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
namespace/knative-eventing unchanged
serviceaccount/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator unchanged
serviceaccount/pingsource-mt-adapter unchanged
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
serviceaccount/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding unchanged
configmap/config-br-default-channel unchanged
configmap/config-br-defaults unchanged
configmap/default-ch-webhook unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
deployment.apps/eventing-controller unchanged
deployment.apps/pingsource-mt-adapter configured
deployment.apps/eventing-webhook unchanged
service/eventing-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver configured
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress unchanged
clusterrole.rbac.authorization.k8s.io/eventing-config-reader unchanged
clusterrole.rbac.authorization.k8s.io/channelable-manipulator configured
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
clusterrole.rbac.authorization.k8s.io/podspecable-binding configured
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding unchanged
clusterrole.rbac.authorization.k8s.io/source-observer configured
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev unchanged
secret/eventing-webhook-certs unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev unchanged
deployment "eventing-controller" successfully rolled out
service/autoscaler annotated
service/autoscaler annotated
service/activator-service annotated
service/activator-service annotated
deployment "eventing-controller" successfully rolled out
deployment "eventing-webhook" successfully rolled out
configmap/config-imc-event-dispatcher created
clusterrole.rbac.authorization.k8s.io/imc-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/imc-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/imc-controller created
serviceaccount/imc-controller created
clusterrole.rbac.authorization.k8s.io/imc-dispatcher created
service/imc-dispatcher created
serviceaccount/imc-dispatcher created
clusterrolebinding.rbac.authorization.k8s.io/imc-controller created
clusterrolebinding.rbac.authorization.k8s.io/imc-dispatcher created
customresourcedefinition.apiextensions.k8s.io/inmemorychannels.messaging.knative.dev created
deployment.apps/imc-controller created
deployment.apps/imc-dispatcher created
deployment "imc-controller" successfully rolled out
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-channel-broker-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
serviceaccount/mt-broker-filter created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
serviceaccount/mt-broker-ingress created
clusterrolebinding.rbac.authorization.k8s.io/eventing-mt-channel-broker-controller created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
deployment.apps/mt-broker-filter created
service/broker-filter created
deployment.apps/mt-broker-ingress created
service/broker-ingress created
deployment.apps/mt-broker-controller created
horizontalpodautoscaler.autoscaling/broker-ingress-hpa created
horizontalpodautoscaler.autoscaling/broker-filter-hpa created
deployment "mt-broker-controller" successfully rolled out
deployment "mt-broker-filter" successfully rolled out
+ '[' true = true ']'
+ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.18.0/serving-default-domain.yaml
job.batch/default-domain created
service/default-domain-service created
+ install_argo
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/argo
+ ./argo.sh
namespace/argo created
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/clusterworkflowtemplates.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/cronworkflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workfloweventbindings.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflowtemplates.argoproj.io created
serviceaccount/argo created
serviceaccount/argo-server created
role.rbac.authorization.k8s.io/argo-role created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-admin created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-edit created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-view created
clusterrole.rbac.authorization.k8s.io/argo-cluster-role created
clusterrole.rbac.authorization.k8s.io/argo-server-cluster-role created
rolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-server-binding created
configmap/workflow-controller-configmap created
service/argo-server created
service/workflow-controller-metrics created
deployment.apps/argo-server created
deployment.apps/workflow-controller created
configmap/workflow-controller-configmap configured
+ install_minio
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/minio
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./minio.sh
TEMPRESOURCES IS /tmp/tempresources
SD_USER_EMAIL IS admin@seldon-ey.io
namespace/minio-system created
"minio" has been added to your repositories
Release "minio" does not exist. Installing it now.
NAME: minio
LAST DEPLOYED: Wed Oct 20 12:13:45 2021
NAMESPACE: minio-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Minio can be accessed via port 9000 on the following DNS name from within your cluster:
minio.minio-system.svc.cluster.local

To access Minio from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace minio-system -l "release=minio" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace minio-system

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access Minio server on http://localhost:9000. Follow the below steps to connect to Minio server with mc client:

  1. Download the Minio mc client - https://docs.minio.io/docs/minio-client-quickstart-guide

  2. Get the ACCESS_KEY=$(kubectl get secret minio -o jsonpath="{.data.accesskey}" | base64 --decode) and the SECRET_KEY=$(kubectl get secret minio -o jsonpath="{.data.secretkey}" | base64 --decode)

  3. mc alias set minio-local http://localhost:9000 "$ACCESS_KEY" "$SECRET_KEY" --api s3v4

  4. mc ls minio-local

Alternately, you can use your browser or the Minio SDK to access the server - https://docs.minio.io/categories/17
virtualservice.networking.istio.io/minio created
+ install_EFK_and_logger
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk
+ export TEMPRESOURCES
+ ./install_efk.sh
TEMPRESOURCES IS /tmp/tempresources
Error from server (AlreadyExists): namespaces "seldon-logs" already exists
namespace seldon-logs exists
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/elastic-credentials created
secret/elastic-credentials created
Cloning into 'opendistro-build'...
remote: Enumerating objects: 7421, done.
remote: Counting objects: 100% (531/531), done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 7421 (delta 343), reused 422 (delta 266), pack-reused 6890
Receiving objects: 100% (7421/7421), 1.90 MiB | 805.00 KiB/s, done.
Resolving deltas: 100% (5084/5084), done.
Fetching origin
Note: switching to 'tags/v1.13.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at aabb00f Modify script and workflow for AMI to include ARM64  (#738)
Successfully packaged chart and saved it to: /tmp/tempresources/opendistro-build/helm/opendistro-es/opendistro-es-1.13.2.tgz
Release "elasticsearch" does not exist. Installing it now.
W1020 12:14:37.341245   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:43.646754   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:44.920126   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:57.940282   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:59.050377   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:59.050983   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
NAME: elasticsearch
LAST DEPLOYED: Wed Oct 20 12:14:34 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
Release "fluentd" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: fluentd
LAST DEPLOYED: Wed Oct 20 12:15:10 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=seldon-logs get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.
Waiting for deployment "elasticsearch-opendistro-es-kibana" rollout to finish: 0 of 1 updated replicas are available...
deployment "elasticsearch-opendistro-es-kibana" successfully rolled out
+ ./eventing_for_logs_ns.sh
broker.eventing.knative.dev/default created
knative broker created
+ kubectl apply -f /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk/kibana-virtualservice.yaml
virtualservice.networking.istio.io/kibana created
+ install_seldon_core
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/seldon-core
+ export TEMPRESOURCES
+ export SELDON_CORE_VERSION
+ export MULTITENANT
+ export EXTERNAL_PROTOCOL
+ ./install_seldon_core.sh
SELDON CORE VERSION v1.9.1
Cloning into 'seldon-core'...
remote: Enumerating objects: 130545, done.
remote: Counting objects: 100% (2898/2898), done.
remote: Compressing objects: 100% (1172/1172), done.
remote: Total 130545 (delta 1846), reused 2511 (delta 1606), pack-reused 127647
Receiving objects: 100% (130545/130545), 212.37 MiB | 824.00 KiB/s, done.
Resolving deltas: 100% (78770/78770), done.
Note: switching to '8ad2ede5ca18e321f8603f1e2a821e767af000de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

using /tmp/tempresources/seldon-core
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
gateway.networking.istio.io/seldon-gateway configured
Release "seldon-core" does not exist. Installing it now.
W1020 12:21:32.726503   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
W1020 12:21:57.693208   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
NAME: seldon-core
LAST DEPLOYED: Wed Oct 20 12:21:13 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
Waiting for deployment "seldon-controller-manager" rollout to finish: 0 of 1 updated replicas are available...
deployment "seldon-controller-manager" successfully rolled out
+ install_analytics
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/prometheus
+ export TEMPRESOURCES
+ ./seldon-core-analytics.sh
configmap/model-usage-rules created
Error from server (NotFound): deployments.apps "seldon-core-analytics-prometheus-seldon" not found
Release "seldon-core-analytics" does not exist. Installing it now.
W1020 12:28:18.796115   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:20.023979   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:49.096327   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:50.323697   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:51.355141   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:52.574403   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:53.599335   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:55.648768   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:56.670352   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:57.676505   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:58.922424   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:00.149772   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:01.379295   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:03.834611   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
W1020 12:29:22.466916   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:22.467337   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:25.947779   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.951773   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.988757   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.994807   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.995223   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:26.358782   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358910   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359018   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358798   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359349   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.767071   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:27.176581   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
NAME: seldon-core-analytics
LAST DEPLOYED: Wed Oct 20 12:28:15 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
+ install_kfserving
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/kfserving
+ export TEMPRESOURCES
+ export KFSERVING_TAG
+ ./install_kfserving.sh
TEMPRESOURCES IS /tmp/tempresources
KFSERVING_TAG v0.4.1
Cloning into 'kfserving'...
remote: Enumerating objects: 44567, done.
remote: Counting objects: 100% (1826/1826), done.
remote: Compressing objects: 100% (1192/1192), done.
remote: Total 44567 (delta 839), reused 1249 (delta 566), pack-reused 42741
Receiving objects: 100% (44567/44567), 116.21 MiB | 800.00 KiB/s, done.
Resolving deltas: 100% (17763/17763), done.
Note: switching to 'f253dd529ba25c080ca458d8dc36fd0a19bbd473'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f253dd52 update 0.4.1 yaml (#1176)
using /tmp/tempresources/kfserving
namespace/kfserving-system created
Warning: resource namespaces/kfserving-system is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/kfserving-system configured
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/inferenceservices.serving.kubeflow.org created
Warning: admissionregistration.k8s.io/v1beta1 MutatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 MutatingWebhookConfiguration
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
role.rbac.authorization.k8s.io/leader-election-role created
clusterrole.rbac.authorization.k8s.io/kfserving-manager-role created
clusterrole.rbac.authorization.k8s.io/kfserving-proxy-role created
rolebinding.rbac.authorization.k8s.io/leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-proxy-rolebinding created
configmap/inferenceservice-config created
secret/kfserving-webhook-server-secret created
service/kfserving-controller-manager-metrics-service created
service/kfserving-controller-manager-service created
service/kfserving-webhook-server-service created
statefulset.apps/kfserving-controller-manager created
Warning: admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Certificate" in version "cert-manager.io/v1alpha2"
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Issuer" in version "cert-manager.io/v1alpha2"
configmap/inferenceservice-config patched
service: kfserving-webhook-server-service
namespace: kfserving-system
secret: kfserving-webhook-server-cert
webhookDeploymentName: kfserving-controller-manager-0
webhookConfigName: inferenceservice.serving.kubeflow.org
creating certs in tmpdir /tmp/tmp.VFjc8KH97E 
Generating RSA private key, 2048 bit long modulus (2 primes)
.......................+++++
...........................................................+++++
e is 65537 (0x010001)
Generating RSA private key, 2048 bit long modulus (2 primes)
........................................................................................+++++
......................................................................+++++
e is 65537 (0x010001)
Signature ok
subject=CN = kfserving-webhook-server-service.kfserving-system.svc
Getting CA Private Key
W1020 12:32:50.683819   37974 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
secret/kfserving-webhook-server-cert created
pod "kfserving-controller-manager-0" deleted
webhook kfserving-controller-manager-0 is restarted to utilize the new secret
CA Certificate:
-----BEGIN CERTIFICATE-----
MIIDYTCCAkmgAwIBAgIUIwKbuXlVEBkLnIHYAy0VIOtbhEIwDQYJKoZIhvcNAQEL
BQAwQDE+MDwGA1UEAww1a2ZzZXJ2aW5nLXdlYmhvb2stc2VydmVyLXNlcnZpY2Uu
a2ZzZXJ2aW5nLXN5c3RlbS5zdmMwHhcNMjExMDIwMDcwMjUwWhcNMjIxMDIwMDcw
MjUwWjBAMT4wPAYDVQQDDDVrZnNlcnZpbmctd2ViaG9vay1zZXJ2ZXItc2Vydmlj
ZS5rZnNlcnZpbmctc3lzdGVtLnN2YzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKqYeLIbze8FaJMmaThqsu9gfXsBwXubosNWODeP9KkN1K0MZhPQc2uJ
5fSwW13cxRaXYnOfaT2AmYdXJZKLBKSWCPPli2rIG9sK0uSm6uR6F/wiXRxlhWHI
R2IXzvbChEczanKCj9WGqolBv2pORYToROmtKxrOmgIx80bwWMKRYARskZtXwUe2
q1OYIsjM0iTMxLgTb1sQs1fXXQ2IgGgYXsonK7FRkcfI7mN0BmcOesOnTw1FAcPO
I7D+FKVZfiQxTY8ktx7WxlszKcmh7hd0KOJC2sHfCUJf82O4h8R/ugtSeS/m1K+n
171KW4DpYccvbKDLA8KotO7nTaN5YXcCAwEAAaNTMFEwHQYDVR0OBBYEFNhFaXMQ
qRjegiNmObr9mZHh4QdtMB8GA1UdIwQYMBaAFNhFaXMQqRjegiNmObr9mZHh4Qdt
MA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAA2wU0Ei06Mrd8hW
yscVL1R0odDF5m2pAVhE2Jgig3Di2gLNaEHT0jjOVSWoDRDyxPy8I0a+KirqlWwA
5/2uQiAE60rTLugKO+xdHgkGp3j/QWK6bczlm4S2b5cD0blv+u0TFbnikbKUFRJ1
EpBuLcKWQJUOEvmgtikYeDEsyLrozu8OnxHXiO1bn2ZRPhnDHvbgNb+IeBaeq+a9
NFoN87NOiqXVTxLUt7W4JhazM8ZuOeEfQUzl7k3Wgle9aY37rviD14MMboPigA74
5OB8HTMrpvcCvvqJaszuxirSwHK+y54rKbuNiHQGbnC384viA/JY9qGD4R1kopu0
W+A9NeU=
-----END CERTIFICATE-----
Encoded CA:
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURZVENDQWttZ0F3SUJBZ0lVSXdLYnVYbFZFQmtMbklIWUF5MFZJT3RiaEVJd0RRWUpLb1pJaHZjTkFRRUwKQlFBd1FERStNRHdHQTFVRUF3dzFhMlp6WlhKMmFXNW5MWGRsWW1odmIyc3RjMlZ5ZG1WeUxYTmxjblpwWTJVdQphMlp6WlhKMmFXNW5MWE41YzNSbGJTNXpkbU13SGhjTk1qRXhNREl3TURjd01qVXdXaGNOTWpJeE1ESXdNRGN3Ck1qVXdXakJBTVQ0d1BBWURWUVFERERWclpuTmxjblpwYm1jdGQyVmlhRzl2YXkxelpYSjJaWEl0YzJWeWRtbGoKWlM1clpuTmxjblpwYm1jdGMzbHpkR1Z0TG5OMll6Q0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQwpBUW9DZ2dFQkFLcVllTEliemU4RmFKTW1hVGhxc3U5Z2ZYc0J3WHVib3NOV09EZVA5S2tOMUswTVpoUFFjMnVKCjVmU3dXMTNjeFJhWFluT2ZhVDJBbVlkWEpaS0xCS1NXQ1BQbGkycklHOXNLMHVTbTZ1UjZGL3dpWFJ4bGhXSEkKUjJJWHp2YkNoRWN6YW5LQ2o5V0dxb2xCdjJwT1JZVG9ST210S3hyT21nSXg4MGJ3V01LUllBUnNrWnRYd1VlMgpxMU9ZSXNqTTBpVE14TGdUYjFzUXMxZlhYUTJJZ0dnWVhzb25LN0ZSa2NmSTdtTjBCbWNPZXNPblR3MUZBY1BPCkk3RCtGS1ZaZmlReFRZOGt0eDdXeGxzektjbWg3aGQwS09KQzJzSGZDVUpmODJPNGg4Ui91Z3RTZVMvbTFLK24KMTcxS1c0RHBZY2N2YktETEE4S290TzduVGFONVlYY0NBd0VBQWFOVE1GRXdIUVlEVlIwT0JCWUVGTmhGYVhNUQpxUmplZ2lObU9icjltWkhoNFFkdE1COEdBMVVkSXdRWU1CYUFGTmhGYVhNUXFSamVnaU5tT2JyOW1aSGg0UWR0Ck1BOEdBMVVkRXdFQi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBMndVMEVpMDZNcmQ4aFcKeXNjVkwxUjBvZERGNW0ycEFWaEUySmdpZzNEaTJnTE5hRUhUMGpqT1ZTV29EUkR5eFB5OEkwYStLaXJxbFd3QQo1LzJ1UWlBRTYwclRMdWdLTyt4ZEhna0dwM2ovUVdLNmJjemxtNFMyYjVjRDBibHYrdTBURmJuaWtiS1VGUkoxCkVwQnVMY0tXUUpVT0V2bWd0aWtZZURFc3lMcm96dThPbnhIWGlPMWJuMlpSUGhuREh2YmdOYitJZUJhZXErYTkKTkZvTjg3Tk9pcVhWVHhMVXQ3VzRKaGF6TThadU9lRWZRVXpsN2szV2dsZTlhWTM3cnZpRDE0TU1ib1BpZ0E3NAo1T0I4SFRNcnB2Y0N2dnFKYXN6dXhpclN3SEsreTU0cktidU5pSFFHYm5DMzg0dmlBL0pZOXFHRDRSMWtvcHUwClcrQTlOZVU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K 

patching ca bundle for mutating webhook configuration...
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
patching ca bundle for validating webhook configuration...
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
+ configure_namespaces
+ kubectl create namespace seldon
namespace/seldon created
+ kubectl label ns seldon seldon.restricted=false --overwrite=true
namespace/seldon labeled
+ kubectl label ns seldon serving.kubeflow.org/inferenceservice=enabled --overwrite=true
namespace/seldon labeled
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/configure-batch-on-ns
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./batch-sa-for-ns.sh
TEMPRESOURCES IS /tmp/tempresources
role.rbac.authorization.k8s.io/workflow created
serviceaccount/workflow created
rolebinding.rbac.authorization.k8s.io/workflow created
secret/seldon-job-secret created
Error from server (NotFound): namespaces "kubeflow" not found
secret/seldon-job-secret configured
configured for minio in minio-system
+ install_postgres
+ '[' true = true ']'
+ echo 'Installing postgres...'
Installing postgres...
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/postgres
+ export TEMPRESOURCES
+ export STARTUP_DIR
+ POSTGRES_MANIFEST=minimal-postgres-manifest.yaml
+ ./install_postgres.sh
Installing zalando postgres operator and a db instance if required
Cloning into 'postgres-operator'...
remote: Enumerating objects: 22250, done.
remote: Counting objects: 100% (2142/2142), done.
remote: Compressing objects: 100% (964/964), done.
remote: Total 22250 (delta 1504), reused 1700 (delta 1145), pack-reused 20108
Receiving objects: 100% (22250/22250), 8.71 MiB | 915.00 KiB/s, done.
Resolving deltas: 100% (15803/15803), done.
Note: switching to 'v1.6.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c18241f1 Bump v1.6.2 (#1433)
namespace/postgres created
Release "postgres-operator" does not exist. Installing it now.
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: postgres-operator
LAST DEPLOYED: Wed Oct 20 12:34:07 2021
NAMESPACE: postgres
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that postgres-operator has started, run:

  kubectl --namespace=postgres get pods -l "app.kubernetes.io/name=postgres-operator"
postgresql.acid.zalan.do/seldon-metadata-storage created
The postgres secret has been created by the operator...
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/metadata-postgres created
+ install_keycloak_auth
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/keycloak
+ ./install_keycloak.sh
Error from server (AlreadyExists): namespaces "seldon-system" already exists
secret/realm-secret created
Release "keycloak" does not exist. Installing it now.
NAME: keycloak
LAST DEPLOYED: Wed Oct 20 12:35:16 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
NOTES:
Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  keycloak-http.seldon-system.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

  export POD_NAME=$(kubectl get pods --namespace seldon-system -l app.kubernetes.io/instance=keycloak -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use Keycloak"
  kubectl port-forward --namespace seldon-system $POD_NAME 8080

Login with the following credentials:
Username: "admin@seldon-ey.io"

To retrieve the initial user password run:
kubectl get secret --namespace seldon-system keycloak-http -o jsonpath="{.data.password}" | base64 --decode; echo
virtualservice.networking.istio.io/keycloak created
Waiting for 1 pods to be ready...
statefulset rolling update complete 1 pods at revision keycloak-5d9666fb66...
Creating default keycloak user
 * Default user created
Creating API auth client
 * API client created
 * Keycloak setup completed
[sepoy@xps seldon-deploy-install]$ ./sd-setup/sd-install-default
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/git-creds configured
namespace/argocd configured
Error from server (AlreadyExists): namespaces "seldon-system" already exists
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/request-logger-auth configured
./sd-setup/sd-install-default: line 80: EXTERNAL_HOST: unbound variable[sepoy@xps seldon-deploy-install]$ ./prerequisites-setup/default-setup.sh
+++ dirname ./prerequisites-setup/default-setup.sh
++ cd ./prerequisites-setup
++ pwd
+ STARTUP_DIR=/home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ SELDON_CORE_DIR=
+ KFSERVING_DIR=
+ SELDON_CORE_VERSION=v1.9.1
+ KFSERVING_TAG=v0.4.1
+ ENABLE_KNATIVE_XIP=true
+ TEMPRESOURCES=/tmp/tempresources
+ SDCONFIG_FILE=/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
+ source /home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
++ GIT_USER=fourtimes
++ GIT_TOKEN=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
++ GIT_EMAIL=jjino@protonmail.com
++ ENABLE_GIT_SSH_CREDS=false
++ SD_USER_EMAIL=admin@seldon-ey.io
++ SD_PASSWORD=ChangeMe@123
++ XTERNAL_HOST=
++ EXTERNAL_PROTOCOL=http
++ KFSERVING_PROTOCOL=http
++ MULTITENANT=false
++ ENABLE_APP_AUTH=true
++ VIRTUALSERVICE_CREATE=true
++ ENABLE_METADATA_POSTGRES=true
++ ENABLE_OPA=false
++ ENABLE_PROJECT_BASED_AUTH=false
++ ENABLE_AUDIT=true
+ ENABLE_METADATA_POSTGRES=true
+ check_creds
+ ((  18 < 8  ))
+ ((  12 < 8  ))
+ setup_tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/clean
removed /tmp/tempresources
+ mkdir -p /tmp/tempresources
+ create_istio
+ cd /tmp/tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/istio/install_istio_new.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   102  100   102    0     0     70      0  0:00:01  0:00:01 --:--:--    70
100  4549  100  4549    0     0   2086      0  0:00:02  0:00:02 --:--:--     0

Downloading istio-1.7.3 from https://github.com/istio/istio/releases/download/1.7.3/istio-1.7.3-linux-amd64.tar.gz ...

Istio 1.7.3 Download Complete!

Istio has been successfully downloaded into the istio-1.7.3 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /tmp/tempresources/istio-1.7.3/bin directory to your environment path variable with:
	 export PATH="$PATH:/tmp/tempresources/istio-1.7.3/bin"

Begin the Istio pre-installation check by running:
	 istioctl x precheck 

Need more information? Visit https://istio.io/latest/docs/setup/install/ 
Installing istio
✔ Istio core installed                                                                                                                                                                        
✔ Istiod installed                                                                                                                                                                            
✔ Addons installed                                                                                                                                                                            
✔ Ingress gateways installed                                                                                                                                                                  
✔ Installation complete                                                                                                                                                                       istio & gateway setup completed
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ wait_istio_ready
+ kubectl rollout status -n istio-system deployment.v1.apps/istio-ingressgateway
deployment "istio-ingressgateway" successfully rolled out
+ configure_https
+ '[' http = https ']'
+ create_knative
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/knative
+ ./install_knative.sh
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev created
namespace/knative-serving created
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-serving-core created
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding created
serviceaccount/controller created
clusterrole.rbac.authorization.k8s.io/knative-serving-admin created
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy created
configmap/config-autoscaler created
configmap/config-defaults created
configmap/config-deployment created
configmap/config-domain created
configmap/config-features created
configmap/config-gc created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-network created
configmap/config-observability created
configmap/config-tracing created
horizontalpodautoscaler.autoscaling/activator created
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb created
deployment.apps/activator created
service/activator-service created
deployment.apps/autoscaler created
service/autoscaler created
deployment.apps/controller created
service/controller created
deployment.apps/webhook created
service/webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev created
secret/webhook-certs created
clusterrole.rbac.authorization.k8s.io/knative-serving-istio created
gateway.networking.istio.io/knative-ingress-gateway created
gateway.networking.istio.io/cluster-local-gateway created
gateway.networking.istio.io/knative-local-gateway created
service/knative-local-gateway created
peerauthentication.security.istio.io/webhook created
peerauthentication.security.istio.io/istio-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev created
secret/istio-webhook-certs created
configmap/config-istio created
deployment.apps/networking-istio created
deployment.apps/istio-webhook created
service/istio-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev created
namespace/knative-eventing created
serviceaccount/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator created
serviceaccount/pingsource-mt-adapter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
serviceaccount/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding created
configmap/config-br-default-channel created
configmap/config-br-defaults created
configmap/default-ch-webhook created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-observability created
configmap/config-tracing created
deployment.apps/eventing-controller created
deployment.apps/pingsource-mt-adapter created
deployment.apps/eventing-webhook created
service/eventing-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver created
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter created
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress created
clusterrole.rbac.authorization.k8s.io/eventing-config-reader created
clusterrole.rbac.authorization.k8s.io/channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
clusterrole.rbac.authorization.k8s.io/podspecable-binding created
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding created
clusterrole.rbac.authorization.k8s.io/source-observer created
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer created
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev created
secret/eventing-webhook-certs created
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev created
Sleep and run again - needed for Kind install as not all CRDs get installed sometimes
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
namespace/knative-serving unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-core unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding unchanged
serviceaccount/controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-admin configured
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy unchanged
configmap/config-autoscaler unchanged
configmap/config-defaults unchanged
configmap/config-deployment unchanged
configmap/config-domain unchanged
configmap/config-features unchanged
configmap/config-gc unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-network unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
horizontalpodautoscaler.autoscaling/activator unchanged
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb configured
deployment.apps/activator configured
service/activator-service unchanged
deployment.apps/autoscaler unchanged
service/autoscaler unchanged
deployment.apps/controller configured
service/controller unchanged
deployment.apps/webhook unchanged
service/webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev unchanged
secret/webhook-certs unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-istio unchanged
gateway.networking.istio.io/knative-ingress-gateway unchanged
gateway.networking.istio.io/cluster-local-gateway unchanged
gateway.networking.istio.io/knative-local-gateway unchanged
service/knative-local-gateway unchanged
peerauthentication.security.istio.io/webhook unchanged
peerauthentication.security.istio.io/istio-webhook unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev unchanged
secret/istio-webhook-certs unchanged
configmap/config-istio unchanged
deployment.apps/networking-istio unchanged
deployment.apps/istio-webhook unchanged
service/istio-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
namespace/knative-eventing unchanged
serviceaccount/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator unchanged
serviceaccount/pingsource-mt-adapter unchanged
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
serviceaccount/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding unchanged
configmap/config-br-default-channel unchanged
configmap/config-br-defaults unchanged
configmap/default-ch-webhook unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
deployment.apps/eventing-controller unchanged
deployment.apps/pingsource-mt-adapter configured
deployment.apps/eventing-webhook unchanged
service/eventing-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver configured
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress unchanged
clusterrole.rbac.authorization.k8s.io/eventing-config-reader unchanged
clusterrole.rbac.authorization.k8s.io/channelable-manipulator configured
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
clusterrole.rbac.authorization.k8s.io/podspecable-binding configured
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding unchanged
clusterrole.rbac.authorization.k8s.io/source-observer configured
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev unchanged
secret/eventing-webhook-certs unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev unchanged
deployment "eventing-controller" successfully rolled out
service/autoscaler annotated
service/autoscaler annotated
service/activator-service annotated
service/activator-service annotated
deployment "eventing-controller" successfully rolled out
deployment "eventing-webhook" successfully rolled out
configmap/config-imc-event-dispatcher created
clusterrole.rbac.authorization.k8s.io/imc-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/imc-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/imc-controller created
serviceaccount/imc-controller created
clusterrole.rbac.authorization.k8s.io/imc-dispatcher created
service/imc-dispatcher created
serviceaccount/imc-dispatcher created
clusterrolebinding.rbac.authorization.k8s.io/imc-controller created
clusterrolebinding.rbac.authorization.k8s.io/imc-dispatcher created
customresourcedefinition.apiextensions.k8s.io/inmemorychannels.messaging.knative.dev created
deployment.apps/imc-controller created
deployment.apps/imc-dispatcher created
deployment "imc-controller" successfully rolled out
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-channel-broker-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
serviceaccount/mt-broker-filter created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
serviceaccount/mt-broker-ingress created
clusterrolebinding.rbac.authorization.k8s.io/eventing-mt-channel-broker-controller created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
deployment.apps/mt-broker-filter created
service/broker-filter created
deployment.apps/mt-broker-ingress created
service/broker-ingress created
deployment.apps/mt-broker-controller created
horizontalpodautoscaler.autoscaling/broker-ingress-hpa created
horizontalpodautoscaler.autoscaling/broker-filter-hpa created
deployment "mt-broker-controller" successfully rolled out
deployment "mt-broker-filter" successfully rolled out
+ '[' true = true ']'
+ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.18.0/serving-default-domain.yaml
job.batch/default-domain created
service/default-domain-service created
+ install_argo
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/argo
+ ./argo.sh
namespace/argo created
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/clusterworkflowtemplates.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/cronworkflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workfloweventbindings.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflowtemplates.argoproj.io created
serviceaccount/argo created
serviceaccount/argo-server created
role.rbac.authorization.k8s.io/argo-role created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-admin created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-edit created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-view created
clusterrole.rbac.authorization.k8s.io/argo-cluster-role created
clusterrole.rbac.authorization.k8s.io/argo-server-cluster-role created
rolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-server-binding created
configmap/workflow-controller-configmap created
service/argo-server created
service/workflow-controller-metrics created
deployment.apps/argo-server created
deployment.apps/workflow-controller created
configmap/workflow-controller-configmap configured
+ install_minio
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/minio
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./minio.sh
TEMPRESOURCES IS /tmp/tempresources
SD_USER_EMAIL IS admin@seldon-ey.io
namespace/minio-system created
"minio" has been added to your repositories
Release "minio" does not exist. Installing it now.
NAME: minio
LAST DEPLOYED: Wed Oct 20 12:13:45 2021
NAMESPACE: minio-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Minio can be accessed via port 9000 on the following DNS name from within your cluster:
minio.minio-system.svc.cluster.local

To access Minio from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace minio-system -l "release=minio" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace minio-system

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access Minio server on http://localhost:9000. Follow the below steps to connect to Minio server with mc client:

  1. Download the Minio mc client - https://docs.minio.io/docs/minio-client-quickstart-guide

  2. Get the ACCESS_KEY=$(kubectl get secret minio -o jsonpath="{.data.accesskey}" | base64 --decode) and the SECRET_KEY=$(kubectl get secret minio -o jsonpath="{.data.secretkey}" | base64 --decode)

  3. mc alias set minio-local http://localhost:9000 "$ACCESS_KEY" "$SECRET_KEY" --api s3v4

  4. mc ls minio-local

Alternately, you can use your browser or the Minio SDK to access the server - https://docs.minio.io/categories/17
virtualservice.networking.istio.io/minio created
+ install_EFK_and_logger
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk
+ export TEMPRESOURCES
+ ./install_efk.sh
TEMPRESOURCES IS /tmp/tempresources
Error from server (AlreadyExists): namespaces "seldon-logs" already exists
namespace seldon-logs exists
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/elastic-credentials created
secret/elastic-credentials created
Cloning into 'opendistro-build'...
remote: Enumerating objects: 7421, done.
remote: Counting objects: 100% (531/531), done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 7421 (delta 343), reused 422 (delta 266), pack-reused 6890
Receiving objects: 100% (7421/7421), 1.90 MiB | 805.00 KiB/s, done.
Resolving deltas: 100% (5084/5084), done.
Fetching origin
Note: switching to 'tags/v1.13.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at aabb00f Modify script and workflow for AMI to include ARM64  (#738)
Successfully packaged chart and saved it to: /tmp/tempresources/opendistro-build/helm/opendistro-es/opendistro-es-1.13.2.tgz
Release "elasticsearch" does not exist. Installing it now.
W1020 12:14:37.341245   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:43.646754   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:44.920126   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:57.940282   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:59.050377   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:59.050983   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
NAME: elasticsearch
LAST DEPLOYED: Wed Oct 20 12:14:34 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
Release "fluentd" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: fluentd
LAST DEPLOYED: Wed Oct 20 12:15:10 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=seldon-logs get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.
Waiting for deployment "elasticsearch-opendistro-es-kibana" rollout to finish: 0 of 1 updated replicas are available...
deployment "elasticsearch-opendistro-es-kibana" successfully rolled out
+ ./eventing_for_logs_ns.sh
broker.eventing.knative.dev/default created
knative broker created
+ kubectl apply -f /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk/kibana-virtualservice.yaml
virtualservice.networking.istio.io/kibana created
+ install_seldon_core
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/seldon-core
+ export TEMPRESOURCES
+ export SELDON_CORE_VERSION
+ export MULTITENANT
+ export EXTERNAL_PROTOCOL
+ ./install_seldon_core.sh
SELDON CORE VERSION v1.9.1
Cloning into 'seldon-core'...
remote: Enumerating objects: 130545, done.
remote: Counting objects: 100% (2898/2898), done.
remote: Compressing objects: 100% (1172/1172), done.
remote: Total 130545 (delta 1846), reused 2511 (delta 1606), pack-reused 127647
Receiving objects: 100% (130545/130545), 212.37 MiB | 824.00 KiB/s, done.
Resolving deltas: 100% (78770/78770), done.
Note: switching to '8ad2ede5ca18e321f8603f1e2a821e767af000de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

using /tmp/tempresources/seldon-core
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
gateway.networking.istio.io/seldon-gateway configured
Release "seldon-core" does not exist. Installing it now.
W1020 12:21:32.726503   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
W1020 12:21:57.693208   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
NAME: seldon-core
LAST DEPLOYED: Wed Oct 20 12:21:13 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
Waiting for deployment "seldon-controller-manager" rollout to finish: 0 of 1 updated replicas are available...
deployment "seldon-controller-manager" successfully rolled out
+ install_analytics
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/prometheus
+ export TEMPRESOURCES
+ ./seldon-core-analytics.sh
configmap/model-usage-rules created
Error from server (NotFound): deployments.apps "seldon-core-analytics-prometheus-seldon" not found
Release "seldon-core-analytics" does not exist. Installing it now.
W1020 12:28:18.796115   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:20.023979   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:49.096327   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:50.323697   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:51.355141   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:52.574403   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:53.599335   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:55.648768   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:56.670352   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:57.676505   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:58.922424   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:00.149772   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:01.379295   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:03.834611   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
W1020 12:29:22.466916   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:22.467337   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:25.947779   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.951773   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.988757   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.994807   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.995223   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:26.358782   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358910   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359018   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358798   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359349   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.767071   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:27.176581   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
NAME: seldon-core-analytics
LAST DEPLOYED: Wed Oct 20 12:28:15 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
+ install_kfserving
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/kfserving
+ export TEMPRESOURCES
+ export KFSERVING_TAG
+ ./install_kfserving.sh
TEMPRESOURCES IS /tmp/tempresources
KFSERVING_TAG v0.4.1
Cloning into 'kfserving'...
remote: Enumerating objects: 44567, done.
remote: Counting objects: 100% (1826/1826), done.
remote: Compressing objects: 100% (1192/1192), done.
remote: Total 44567 (delta 839), reused 1249 (delta 566), pack-reused 42741
Receiving objects: 100% (44567/44567), 116.21 MiB | 800.00 KiB/s, done.
Resolving deltas: 100% (17763/17763), done.
Note: switching to 'f253dd529ba25c080ca458d8dc36fd0a19bbd473'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f253dd52 update 0.4.1 yaml (#1176)
using /tmp/tempresources/kfserving
namespace/kfserving-system created
Warning: resource namespaces/kfserving-system is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/kfserving-system configured
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/inferenceservices.serving.kubeflow.org created
Warning: admissionregistration.k8s.io/v1beta1 MutatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 MutatingWebhookConfiguration
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
role.rbac.authorization.k8s.io/leader-election-role created
clusterrole.rbac.authorization.k8s.io/kfserving-manager-role created
clusterrole.rbac.authorization.k8s.io/kfserving-proxy-role created
rolebinding.rbac.authorization.k8s.io/leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-proxy-rolebinding created
configmap/inferenceservice-config created
secret/kfserving-webhook-server-secret created
service/kfserving-controller-manager-metrics-service created
service/kfserving-controller-manager-service created
service/kfserving-webhook-server-service created
statefulset.apps/kfserving-controller-manager created
Warning: admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Certificate" in version "cert-manager.io/v1alpha2"
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Issuer" in version "cert-manager.io/v1alpha2"
configmap/inferenceservice-config patched
service: kfserving-webhook-server-service
namespace: kfserving-system
secret: kfserving-webhook-server-cert
webhookDeploymentName: kfserving-controller-manager-0
webhookConfigName: inferenceservice.serving.kubeflow.org
creating certs in tmpdir /tmp/tmp.VFjc8KH97E 
Generating RSA private key, 2048 bit long modulus (2 primes)
.......................+++++
...........................................................+++++
e is 65537 (0x010001)
Generating RSA private key, 2048 bit long modulus (2 primes)
........................................................................................+++++
......................................................................+++++
e is 65537 (0x010001)
Signature ok
subject=CN = kfserving-webhook-server-service.kfserving-system.svc
Getting CA Private Key
W1020 12:32:50.683819   37974 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
secret/kfserving-webhook-server-cert created
pod "kfserving-controller-manager-0" deleted
webhook kfserving-controller-manager-0 is restarted to utilize the new secret
CA Certificate:
-----BEGIN CERTIFICATE-----
MIIDYTCCAkmgAwIBAgIUIwKbuXlVEBkLnIHYAy0VIOtbhEIwDQYJKoZIhvcNAQEL
BQAwQDE+MDwGA1UEAww1a2ZzZXJ2aW5nLXdlYmhvb2stc2VydmVyLXNlcnZpY2Uu
a2ZzZXJ2aW5nLXN5c3RlbS5zdmMwHhcNMjExMDIwMDcwMjUwWhcNMjIxMDIwMDcw
MjUwWjBAMT4wPAYDVQQDDDVrZnNlcnZpbmctd2ViaG9vay1zZXJ2ZXItc2Vydmlj
ZS5rZnNlcnZpbmctc3lzdGVtLnN2YzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKqYeLIbze8FaJMmaThqsu9gfXsBwXubosNWODeP9KkN1K0MZhPQc2uJ
5fSwW13cxRaXYnOfaT2AmYdXJZKLBKSWCPPli2rIG9sK0uSm6uR6F/wiXRxlhWHI
R2IXzvbChEczanKCj9WGqolBv2pORYToROmtKxrOmgIx80bwWMKRYARskZtXwUe2
q1OYIsjM0iTMxLgTb1sQs1fXXQ2IgGgYXsonK7FRkcfI7mN0BmcOesOnTw1FAcPO
I7D+FKVZfiQxTY8ktx7WxlszKcmh7hd0KOJC2sHfCUJf82O4h8R/ugtSeS/m1K+n
171KW4DpYccvbKDLA8KotO7nTaN5YXcCAwEAAaNTMFEwHQYDVR0OBBYEFNhFaXMQ
qRjegiNmObr9mZHh4QdtMB8GA1UdIwQYMBaAFNhFaXMQqRjegiNmObr9mZHh4Qdt
MA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAA2wU0Ei06Mrd8hW
yscVL1R0odDF5m2pAVhE2Jgig3Di2gLNaEHT0jjOVSWoDRDyxPy8I0a+KirqlWwA
5/2uQiAE60rTLugKO+xdHgkGp3j/QWK6bczlm4S2b5cD0blv+u0TFbnikbKUFRJ1
EpBuLcKWQJUOEvmgtikYeDEsyLrozu8OnxHXiO1bn2ZRPhnDHvbgNb+IeBaeq+a9
NFoN87NOiqXVTxLUt7W4JhazM8ZuOeEfQUzl7k3Wgle9aY37rviD14MMboPigA74
5OB8HTMrpvcCvvqJaszuxirSwHK+y54rKbuNiHQGbnC384viA/JY9qGD4R1kopu0
W+A9NeU=
-----END CERTIFICATE-----
Encoded CA:
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURZVENDQWttZ0F3SUJBZ0lVSXdLYnVYbFZFQmtMbklIWUF5MFZJT3RiaEVJd0RRWUpLb1pJaHZjTkFRRUwKQlFBd1FERStNRHdHQTFVRUF3dzFhMlp6WlhKMmFXNW5MWGRsWW1odmIyc3RjMlZ5ZG1WeUxYTmxjblpwWTJVdQphMlp6WlhKMmFXNW5MWE41YzNSbGJTNXpkbU13SGhjTk1qRXhNREl3TURjd01qVXdXaGNOTWpJeE1ESXdNRGN3Ck1qVXdXakJBTVQ0d1BBWURWUVFERERWclpuTmxjblpwYm1jdGQyVmlhRzl2YXkxelpYSjJaWEl0YzJWeWRtbGoKWlM1clpuTmxjblpwYm1jdGMzbHpkR1Z0TG5OMll6Q0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQwpBUW9DZ2dFQkFLcVllTEliemU4RmFKTW1hVGhxc3U5Z2ZYc0J3WHVib3NOV09EZVA5S2tOMUswTVpoUFFjMnVKCjVmU3dXMTNjeFJhWFluT2ZhVDJBbVlkWEpaS0xCS1NXQ1BQbGkycklHOXNLMHVTbTZ1UjZGL3dpWFJ4bGhXSEkKUjJJWHp2YkNoRWN6YW5LQ2o5V0dxb2xCdjJwT1JZVG9ST210S3hyT21nSXg4MGJ3V01LUllBUnNrWnRYd1VlMgpxMU9ZSXNqTTBpVE14TGdUYjFzUXMxZlhYUTJJZ0dnWVhzb25LN0ZSa2NmSTdtTjBCbWNPZXNPblR3MUZBY1BPCkk3RCtGS1ZaZmlReFRZOGt0eDdXeGxzektjbWg3aGQwS09KQzJzSGZDVUpmODJPNGg4Ui91Z3RTZVMvbTFLK24KMTcxS1c0RHBZY2N2YktETEE4S290TzduVGFONVlYY0NBd0VBQWFOVE1GRXdIUVlEVlIwT0JCWUVGTmhGYVhNUQpxUmplZ2lObU9icjltWkhoNFFkdE1COEdBMVVkSXdRWU1CYUFGTmhGYVhNUXFSamVnaU5tT2JyOW1aSGg0UWR0Ck1BOEdBMVVkRXdFQi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBMndVMEVpMDZNcmQ4aFcKeXNjVkwxUjBvZERGNW0ycEFWaEUySmdpZzNEaTJnTE5hRUhUMGpqT1ZTV29EUkR5eFB5OEkwYStLaXJxbFd3QQo1LzJ1UWlBRTYwclRMdWdLTyt4ZEhna0dwM2ovUVdLNmJjemxtNFMyYjVjRDBibHYrdTBURmJuaWtiS1VGUkoxCkVwQnVMY0tXUUpVT0V2bWd0aWtZZURFc3lMcm96dThPbnhIWGlPMWJuMlpSUGhuREh2YmdOYitJZUJhZXErYTkKTkZvTjg3Tk9pcVhWVHhMVXQ3VzRKaGF6TThadU9lRWZRVXpsN2szV2dsZTlhWTM3cnZpRDE0TU1ib1BpZ0E3NAo1T0I4SFRNcnB2Y0N2dnFKYXN6dXhpclN3SEsreTU0cktidU5pSFFHYm5DMzg0dmlBL0pZOXFHRDRSMWtvcHUwClcrQTlOZVU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K 

patching ca bundle for mutating webhook configuration...
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
patching ca bundle for validating webhook configuration...
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
+ configure_namespaces
+ kubectl create namespace seldon
namespace/seldon created
+ kubectl label ns seldon seldon.restricted=false --overwrite=true
namespace/seldon labeled
+ kubectl label ns seldon serving.kubeflow.org/inferenceservice=enabled --overwrite=true
namespace/seldon labeled
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/configure-batch-on-ns
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./batch-sa-for-ns.sh
TEMPRESOURCES IS /tmp/tempresources
role.rbac.authorization.k8s.io/workflow created
serviceaccount/workflow created
rolebinding.rbac.authorization.k8s.io/workflow created
secret/seldon-job-secret created
Error from server (NotFound): namespaces "kubeflow" not found
secret/seldon-job-secret configured
configured for minio in minio-system
+ install_postgres
+ '[' true = true ']'
+ echo 'Installing postgres...'
Installing postgres...
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/postgres
+ export TEMPRESOURCES
+ export STARTUP_DIR
+ POSTGRES_MANIFEST=minimal-postgres-manifest.yaml
+ ./install_postgres.sh
Installing zalando postgres operator and a db instance if required
Cloning into 'postgres-operator'...
remote: Enumerating objects: 22250, done.
remote: Counting objects: 100% (2142/2142), done.
remote: Compressing objects: 100% (964/964), done.
remote: Total 22250 (delta 1504), reused 1700 (delta 1145), pack-reused 20108
Receiving objects: 100% (22250/22250), 8.71 MiB | 915.00 KiB/s, done.
Resolving deltas: 100% (15803/15803), done.
Note: switching to 'v1.6.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c18241f1 Bump v1.6.2 (#1433)
namespace/postgres created
Release "postgres-operator" does not exist. Installing it now.
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: postgres-operator
LAST DEPLOYED: Wed Oct 20 12:34:07 2021
NAMESPACE: postgres
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that postgres-operator has started, run:

  kubectl --namespace=postgres get pods -l "app.kubernetes.io/name=postgres-operator"
postgresql.acid.zalan.do/seldon-metadata-storage created
The postgres secret has been created by the operator...
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/metadata-postgres created
+ install_keycloak_auth
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/keycloak
+ ./install_keycloak.sh
Error from server (AlreadyExists): namespaces "seldon-system" already exists
secret/realm-secret created
Release "keycloak" does not exist. Installing it now.
NAME: keycloak
LAST DEPLOYED: Wed Oct 20 12:35:16 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
NOTES:
Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  keycloak-http.seldon-system.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

  export POD_NAME=$(kubectl get pods --namespace seldon-system -l app.kubernetes.io/instance=keycloak -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use Keycloak"
  kubectl port-forward --namespace seldon-system $POD_NAME 8080

Login with the following credentials:
Username: "admin@seldon-ey.io"

To retrieve the initial user password run:
kubectl get secret --namespace seldon-system keycloak-http -o jsonpath="{.data.password}" | base64 --decode; echo
virtualservice.networking.istio.io/keycloak created
Waiting for 1 pods to be ready...
statefulset rolling update complete 1 pods at revision keycloak-5d9666fb66...
Creating default keycloak user
 * Default user created
Creating API auth client
 * API client created
 * Keycloak setup completed
[sepoy@xps seldon-deploy-install]$ ./sd-setup/sd-install-default
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/git-creds configured
namespace/argocd configured
Error from server (AlreadyExists): namespaces "seldon-system" already exists
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/request-logger-auth configured
./sd-setup/sd-install-default: line 80: EXTERNAL_HOST: unbound variable
[sepoy@xps seldon-deploy-install]$ ./sd-setup/show-seldon-deploy-url
http://a38fbee579f06403bb22116c69dcb22d-972759690.us-east-2.elb.amazonaws.com/seldon-deploy/
[sepoy@xps seldon-deploy-install]$ ./prerequisites-setup/default-setup.sh
+++ dirname ./prerequisites-setup/default-setup.sh
++ cd ./prerequisites-setup
++ pwd
+ STARTUP_DIR=/home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ SELDON_CORE_DIR=
+ KFSERVING_DIR=
+ SELDON_CORE_VERSION=v1.9.1
+ KFSERVING_TAG=v0.4.1
+ ENABLE_KNATIVE_XIP=true
+ TEMPRESOURCES=/tmp/tempresources
+ SDCONFIG_FILE=/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
+ source /home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
++ GIT_USER=fourtimes
++ GIT_TOKEN=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
++ GIT_EMAIL=jjino@protonmail.com
++ ENABLE_GIT_SSH_CREDS=false
++ SD_USER_EMAIL=admin@seldon-ey.io
++ SD_PASSWORD=ChangeMe@123
++ XTERNAL_HOST=
++ EXTERNAL_PROTOCOL=http
++ KFSERVING_PROTOCOL=http
++ MULTITENANT=false
++ ENABLE_APP_AUTH=true
++ VIRTUALSERVICE_CREATE=true
++ ENABLE_METADATA_POSTGRES=true
++ ENABLE_OPA=false
++ ENABLE_PROJECT_BASED_AUTH=false
++ ENABLE_AUDIT=true
+ ENABLE_METADATA_POSTGRES=true
+ check_creds
+ ((  18 < 8  ))
+ ((  12 < 8  ))
+ setup_tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/clean
removed /tmp/tempresources
+ mkdir -p /tmp/tempresources
+ create_istio
+ cd /tmp/tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/istio/install_istio_new.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   102  100   102    0     0     70      0  0:00:01  0:00:01 --:--:--    70
100  4549  100  4549    0     0   2086      0  0:00:02  0:00:02 --:--:--     0

Downloading istio-1.7.3 from https://github.com/istio/istio/releases/download/1.7.3/istio-1.7.3-linux-amd64.tar.gz ...

Istio 1.7.3 Download Complete!

Istio has been successfully downloaded into the istio-1.7.3 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /tmp/tempresources/istio-1.7.3/bin directory to your environment path variable with:
	 export PATH="$PATH:/tmp/tempresources/istio-1.7.3/bin"

Begin the Istio pre-installation check by running:
	 istioctl x precheck 

Need more information? Visit https://istio.io/latest/docs/setup/install/ 
Installing istio
✔ Istio core installed                                                                                                                                                                        
✔ Istiod installed                                                                                                                                                                            
✔ Addons installed                                                                                                                                                                            
✔ Ingress gateways installed                                                                                                                                                                  
✔ Installation complete                                                                                                                                                                       istio & gateway setup completed
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ wait_istio_ready
+ kubectl rollout status -n istio-system deployment.v1.apps/istio-ingressgateway
deployment "istio-ingressgateway" successfully rolled out
+ configure_https
+ '[' http = https ']'
+ create_knative
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/knative
+ ./install_knative.sh
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev created
namespace/knative-serving created
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-serving-core created
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding created
serviceaccount/controller created
clusterrole.rbac.authorization.k8s.io/knative-serving-admin created
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy created
configmap/config-autoscaler created
configmap/config-defaults created
configmap/config-deployment created
configmap/config-domain created
configmap/config-features created
configmap/config-gc created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-network created
configmap/config-observability created
configmap/config-tracing created
horizontalpodautoscaler.autoscaling/activator created
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb created
deployment.apps/activator created
service/activator-service created
deployment.apps/autoscaler created
service/autoscaler created
deployment.apps/controller created
service/controller created
deployment.apps/webhook created
service/webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev created
secret/webhook-certs created
clusterrole.rbac.authorization.k8s.io/knative-serving-istio created
gateway.networking.istio.io/knative-ingress-gateway created
gateway.networking.istio.io/cluster-local-gateway created
gateway.networking.istio.io/knative-local-gateway created
service/knative-local-gateway created
peerauthentication.security.istio.io/webhook created
peerauthentication.security.istio.io/istio-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev created
secret/istio-webhook-certs created
configmap/config-istio created
deployment.apps/networking-istio created
deployment.apps/istio-webhook created
service/istio-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev created
namespace/knative-eventing created
serviceaccount/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator created
serviceaccount/pingsource-mt-adapter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
serviceaccount/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding created
configmap/config-br-default-channel created
configmap/config-br-defaults created
configmap/default-ch-webhook created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-observability created
configmap/config-tracing created
deployment.apps/eventing-controller created
deployment.apps/pingsource-mt-adapter created
deployment.apps/eventing-webhook created
service/eventing-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver created
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter created
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress created
clusterrole.rbac.authorization.k8s.io/eventing-config-reader created
clusterrole.rbac.authorization.k8s.io/channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
clusterrole.rbac.authorization.k8s.io/podspecable-binding created
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding created
clusterrole.rbac.authorization.k8s.io/source-observer created
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer created
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev created
secret/eventing-webhook-certs created
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev created
Sleep and run again - needed for Kind install as not all CRDs get installed sometimes
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
namespace/knative-serving unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-core unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding unchanged
serviceaccount/controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-admin configured
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy unchanged
configmap/config-autoscaler unchanged
configmap/config-defaults unchanged
configmap/config-deployment unchanged
configmap/config-domain unchanged
configmap/config-features unchanged
configmap/config-gc unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-network unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
horizontalpodautoscaler.autoscaling/activator unchanged
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb configured
deployment.apps/activator configured
service/activator-service unchanged
deployment.apps/autoscaler unchanged
service/autoscaler unchanged
deployment.apps/controller configured
service/controller unchanged
deployment.apps/webhook unchanged
service/webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev unchanged
secret/webhook-certs unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-istio unchanged
gateway.networking.istio.io/knative-ingress-gateway unchanged
gateway.networking.istio.io/cluster-local-gateway unchanged
gateway.networking.istio.io/knative-local-gateway unchanged
service/knative-local-gateway unchanged
peerauthentication.security.istio.io/webhook unchanged
peerauthentication.security.istio.io/istio-webhook unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev unchanged
secret/istio-webhook-certs unchanged
configmap/config-istio unchanged
deployment.apps/networking-istio unchanged
deployment.apps/istio-webhook unchanged
service/istio-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
namespace/knative-eventing unchanged
serviceaccount/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator unchanged
serviceaccount/pingsource-mt-adapter unchanged
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
serviceaccount/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding unchanged
configmap/config-br-default-channel unchanged
configmap/config-br-defaults unchanged
configmap/default-ch-webhook unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
deployment.apps/eventing-controller unchanged
deployment.apps/pingsource-mt-adapter configured
deployment.apps/eventing-webhook unchanged
service/eventing-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver configured
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress unchanged
clusterrole.rbac.authorization.k8s.io/eventing-config-reader unchanged
clusterrole.rbac.authorization.k8s.io/channelable-manipulator configured
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
clusterrole.rbac.authorization.k8s.io/podspecable-binding configured
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding unchanged
clusterrole.rbac.authorization.k8s.io/source-observer configured
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev unchanged
secret/eventing-webhook-certs unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev unchanged
deployment "eventing-controller" successfully rolled out
service/autoscaler annotated
service/autoscaler annotated
service/activator-service annotated
service/activator-service annotated
deployment "eventing-controller" successfully rolled out
deployment "eventing-webhook" successfully rolled out
configmap/config-imc-event-dispatcher created
clusterrole.rbac.authorization.k8s.io/imc-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/imc-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/imc-controller created
serviceaccount/imc-controller created
clusterrole.rbac.authorization.k8s.io/imc-dispatcher created
service/imc-dispatcher created
serviceaccount/imc-dispatcher created
clusterrolebinding.rbac.authorization.k8s.io/imc-controller created
clusterrolebinding.rbac.authorization.k8s.io/imc-dispatcher created
customresourcedefinition.apiextensions.k8s.io/inmemorychannels.messaging.knative.dev created
deployment.apps/imc-controller created
deployment.apps/imc-dispatcher created
deployment "imc-controller" successfully rolled out
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-channel-broker-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
serviceaccount/mt-broker-filter created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
serviceaccount/mt-broker-ingress created
clusterrolebinding.rbac.authorization.k8s.io/eventing-mt-channel-broker-controller created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
deployment.apps/mt-broker-filter created
service/broker-filter created
deployment.apps/mt-broker-ingress created
service/broker-ingress created
deployment.apps/mt-broker-controller created
horizontalpodautoscaler.autoscaling/broker-ingress-hpa created
horizontalpodautoscaler.autoscaling/broker-filter-hpa created
deployment "mt-broker-controller" successfully rolled out
deployment "mt-broker-filter" successfully rolled out
+ '[' true = true ']'
+ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.18.0/serving-default-domain.yaml
job.batch/default-domain created
service/default-domain-service created
+ install_argo
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/argo
+ ./argo.sh
namespace/argo created
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/clusterworkflowtemplates.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/cronworkflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workfloweventbindings.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflowtemplates.argoproj.io created
serviceaccount/argo created
serviceaccount/argo-server created
role.rbac.authorization.k8s.io/argo-role created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-admin created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-edit created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-view created
clusterrole.rbac.authorization.k8s.io/argo-cluster-role created
clusterrole.rbac.authorization.k8s.io/argo-server-cluster-role created
rolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-server-binding created
configmap/workflow-controller-configmap created
service/argo-server created
service/workflow-controller-metrics created
deployment.apps/argo-server created
deployment.apps/workflow-controller created
configmap/workflow-controller-configmap configured
+ install_minio
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/minio
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./minio.sh
TEMPRESOURCES IS /tmp/tempresources
SD_USER_EMAIL IS admin@seldon-ey.io
namespace/minio-system created
"minio" has been added to your repositories
Release "minio" does not exist. Installing it now.
NAME: minio
LAST DEPLOYED: Wed Oct 20 12:13:45 2021
NAMESPACE: minio-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Minio can be accessed via port 9000 on the following DNS name from within your cluster:
minio.minio-system.svc.cluster.local

To access Minio from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace minio-system -l "release=minio" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace minio-system

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access Minio server on http://localhost:9000. Follow the below steps to connect to Minio server with mc client:

  1. Download the Minio mc client - https://docs.minio.io/docs/minio-client-quickstart-guide

  2. Get the ACCESS_KEY=$(kubectl get secret minio -o jsonpath="{.data.accesskey}" | base64 --decode) and the SECRET_KEY=$(kubectl get secret minio -o jsonpath="{.data.secretkey}" | base64 --decode)

  3. mc alias set minio-local http://localhost:9000 "$ACCESS_KEY" "$SECRET_KEY" --api s3v4

  4. mc ls minio-local

Alternately, you can use your browser or the Minio SDK to access the server - https://docs.minio.io/categories/17
virtualservice.networking.istio.io/minio created
+ install_EFK_and_logger
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk
+ export TEMPRESOURCES
+ ./install_efk.sh
TEMPRESOURCES IS /tmp/tempresources
Error from server (AlreadyExists): namespaces "seldon-logs" already exists
namespace seldon-logs exists
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/elastic-credentials created
secret/elastic-credentials created
Cloning into 'opendistro-build'...
remote: Enumerating objects: 7421, done.
remote: Counting objects: 100% (531/531), done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 7421 (delta 343), reused 422 (delta 266), pack-reused 6890
Receiving objects: 100% (7421/7421), 1.90 MiB | 805.00 KiB/s, done.
Resolving deltas: 100% (5084/5084), done.
Fetching origin
Note: switching to 'tags/v1.13.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at aabb00f Modify script and workflow for AMI to include ARM64  (#738)
Successfully packaged chart and saved it to: /tmp/tempresources/opendistro-build/helm/opendistro-es/opendistro-es-1.13.2.tgz
Release "elasticsearch" does not exist. Installing it now.
W1020 12:14:37.341245   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:43.646754   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:44.920126   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:57.940282   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:59.050377   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:59.050983   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
NAME: elasticsearch
LAST DEPLOYED: Wed Oct 20 12:14:34 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
Release "fluentd" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: fluentd
LAST DEPLOYED: Wed Oct 20 12:15:10 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=seldon-logs get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.
Waiting for deployment "elasticsearch-opendistro-es-kibana" rollout to finish: 0 of 1 updated replicas are available...
deployment "elasticsearch-opendistro-es-kibana" successfully rolled out
+ ./eventing_for_logs_ns.sh
broker.eventing.knative.dev/default created
knative broker created
+ kubectl apply -f /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk/kibana-virtualservice.yaml
virtualservice.networking.istio.io/kibana created
+ install_seldon_core
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/seldon-core
+ export TEMPRESOURCES
+ export SELDON_CORE_VERSION
+ export MULTITENANT
+ export EXTERNAL_PROTOCOL
+ ./install_seldon_core.sh
SELDON CORE VERSION v1.9.1
Cloning into 'seldon-core'...
remote: Enumerating objects: 130545, done.
remote: Counting objects: 100% (2898/2898), done.
remote: Compressing objects: 100% (1172/1172), done.
remote: Total 130545 (delta 1846), reused 2511 (delta 1606), pack-reused 127647
Receiving objects: 100% (130545/130545), 212.37 MiB | 824.00 KiB/s, done.
Resolving deltas: 100% (78770/78770), done.
Note: switching to '8ad2ede5ca18e321f8603f1e2a821e767af000de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

using /tmp/tempresources/seldon-core
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
gateway.networking.istio.io/seldon-gateway configured
Release "seldon-core" does not exist. Installing it now.
W1020 12:21:32.726503   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
W1020 12:21:57.693208   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
NAME: seldon-core
LAST DEPLOYED: Wed Oct 20 12:21:13 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
Waiting for deployment "seldon-controller-manager" rollout to finish: 0 of 1 updated replicas are available...
deployment "seldon-controller-manager" successfully rolled out
+ install_analytics
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/prometheus
+ export TEMPRESOURCES
+ ./seldon-core-analytics.sh
configmap/model-usage-rules created
Error from server (NotFound): deployments.apps "seldon-core-analytics-prometheus-seldon" not found
Release "seldon-core-analytics" does not exist. Installing it now.
W1020 12:28:18.796115   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:20.023979   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:49.096327   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:50.323697   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:51.355141   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:52.574403   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:53.599335   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:55.648768   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:56.670352   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
[sepoy@xps seldon-deploy-install]$ ./prerequisites-setup/default-setup.sh
+++ dirname ./prerequisites-setup/default-setup.sh
++ cd ./prerequisites-setup
++ pwd
+ STARTUP_DIR=/home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ SELDON_CORE_DIR=
+ KFSERVING_DIR=
+ SELDON_CORE_VERSION=v1.9.1
+ KFSERVING_TAG=v0.4.1
+ ENABLE_KNATIVE_XIP=true
+ TEMPRESOURCES=/tmp/tempresources
+ SDCONFIG_FILE=/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
+ source /home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
++ GIT_USER=four[sepoy@xps seldon-deploy-install]$ ./prerequisites-setup/default-setup.sh
+++ dirname ./prerequisites-setup/default-setup.sh
++ cd ./prerequisites-setup
++ pwd
+ STARTUP_DIR=/home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ SELDON_CORE_DIR=
+ KFSERVING_DIR=
+ SELDON_CORE_VERSION=v1.9.1
+ KFSERVING_TAG=v0.4.1
+ ENABLE_KNATIVE_XIP=true
+ TEMPRESOURCES=/tmp/tempresources
+ SDCONFIG_FILE=/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
+ source /home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
++ GIT_USER=fourtimes
++ GIT_TOKEN=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
++ GIT_EMAIL=jjino@protonmail.com
++ ENABLE_GIT_SSH_CREDS=false
++ SD_USER_EMAIL=admin@seldon-ey.io
++ SD_PASSWORD=ChangeMe@123
++ XTERNAL_HOST=
++ EXTERNAL_PROTOCOL=http
++ KFSERVING_PROTOCOL=http
++ MULTITENANT=false
++ ENABLE_APP_AUTH=true
++ VIRTUALSERVICE_CREATE=true
++ ENABLE_METADATA_POSTGRES=true
++ ENABLE_OPA=false
++ ENABLE_PROJECT_BASED_AUTH=false
++ ENABLE_AUDIT=true
+ ENABLE_METADATA_POSTGRES=true
+ check_creds
+ ((  18 < 8  ))
+ ((  12 < 8  ))
+ setup_tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/clean
removed /tmp/tempresources
+ mkdir -p /tmp/tempresources
+ create_istio
+ cd /tmp/tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/istio/install_istio_new.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   102  100   102    0     0     70      0  0:00:01  0:00:01 --:--:--    70
100  4549  100  4549    0     0   2086      0  0:00:02  0:00:02 --:--:--     0

Downloading istio-1.7.3 from https://github.com/istio/istio/releases/download/1.7.3/istio-1.7.3-linux-amd64.tar.gz ...

Istio 1.7.3 Download Complete!

Istio has been successfully downloaded into the istio-1.7.3 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /tmp/tempresources/istio-1.7.3/bin directory to your environment path variable with:
	 export PATH="$PATH:/tmp/tempresources/istio-1.7.3/bin"

Begin the Istio pre-installation check by running:
	 istioctl x precheck 

Need more information? Visit https://istio.io/latest/docs/setup/install/ 
Installing istio
✔ Istio core installed                                                                                                                                                                        
✔ Istiod installed                                                                                                                                                                            
✔ Addons installed                                                                                                                                                                            
✔ Ingress gateways installed                                                                                                                                                                  
✔ Installation complete                                                                                                                                                                       istio & gateway setup completed
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ wait_istio_ready
+ kubectl rollout status -n istio-system deployment.v1.apps/istio-ingressgateway
deployment "istio-ingressgateway" successfully rolled out
+ configure_https
+ '[' http = https ']'
+ create_knative
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/knative
+ ./install_knative.sh
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev created
namespace/knative-serving created
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-serving-core created
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding created
serviceaccount/controller created
clusterrole.rbac.authorization.k8s.io/knative-serving-admin created
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy created
configmap/config-autoscaler created
configmap/config-defaults created
configmap/config-deployment created
configmap/config-domain created
configmap/config-features created
configmap/config-gc created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-network created
configmap/config-observability created
configmap/config-tracing created
horizontalpodautoscaler.autoscaling/activator created
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb created
deployment.apps/activator created
service/activator-service created
deployment.apps/autoscaler created
service/autoscaler created
deployment.apps/controller created
service/controller created
deployment.apps/webhook created
service/webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev created
secret/webhook-certs created
clusterrole.rbac.authorization.k8s.io/knative-serving-istio created
gateway.networking.istio.io/knative-ingress-gateway created
gateway.networking.istio.io/cluster-local-gateway created
gateway.networking.istio.io/knative-local-gateway created
service/knative-local-gateway created
peerauthentication.security.istio.io/webhook created
peerauthentication.security.istio.io/istio-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev created
secret/istio-webhook-certs created
configmap/config-istio created
deployment.apps/networking-istio created
deployment.apps/istio-webhook created
service/istio-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev created
namespace/knative-eventing created
serviceaccount/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator created
serviceaccount/pingsource-mt-adapter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
serviceaccount/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding created
configmap/config-br-default-channel created
configmap/config-br-defaults created
configmap/default-ch-webhook created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-observability created
configmap/config-tracing created
deployment.apps/eventing-controller created
deployment.apps/pingsource-mt-adapter created
deployment.apps/eventing-webhook created
service/eventing-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver created
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter created
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress created
clusterrole.rbac.authorization.k8s.io/eventing-config-reader created
clusterrole.rbac.authorization.k8s.io/channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
clusterrole.rbac.authorization.k8s.io/podspecable-binding created
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding created
clusterrole.rbac.authorization.k8s.io/source-observer created
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer created
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev created
secret/eventing-webhook-certs created
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev created
Sleep and run again - needed for Kind install as not all CRDs get installed sometimes
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
namespace/knative-serving unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-core unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding unchanged
serviceaccount/controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-admin configured
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy unchanged
configmap/config-autoscaler unchanged
configmap/config-defaults unchanged
configmap/config-deployment unchanged
configmap/config-domain unchanged
configmap/config-features unchanged
configmap/config-gc unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-network unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
horizontalpodautoscaler.autoscaling/activator unchanged
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb configured
deployment.apps/activator configured
service/activator-service unchanged
deployment.apps/autoscaler unchanged
service/autoscaler unchanged
deployment.apps/controller configured
service/controller unchanged
deployment.apps/webhook unchanged
service/webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev unchanged
secret/webhook-certs unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-istio unchanged
gateway.networking.istio.io/knative-ingress-gateway unchanged
gateway.networking.istio.io/cluster-local-gateway unchanged
gateway.networking.istio.io/knative-local-gateway unchanged
service/knative-local-gateway unchanged
peerauthentication.security.istio.io/webhook unchanged
peerauthentication.security.istio.io/istio-webhook unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev unchanged
secret/istio-webhook-certs unchanged
configmap/config-istio unchanged
deployment.apps/networking-istio unchanged
deployment.apps/istio-webhook unchanged
service/istio-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
namespace/knative-eventing unchanged
serviceaccount/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator unchanged
serviceaccount/pingsource-mt-adapter unchanged
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
serviceaccount/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding unchanged
configmap/config-br-default-channel unchanged
configmap/config-br-defaults unchanged
configmap/default-ch-webhook unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
deployment.apps/eventing-controller unchanged
deployment.apps/pingsource-mt-adapter configured
deployment.apps/eventing-webhook unchanged
service/eventing-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver configured
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress unchanged
clusterrole.rbac.authorization.k8s.io/eventing-config-reader unchanged
clusterrole.rbac.authorization.k8s.io/channelable-manipulator configured
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
clusterrole.rbac.authorization.k8s.io/podspecable-binding configured
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding unchanged
clusterrole.rbac.authorization.k8s.io/source-observer configured
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev unchanged
secret/eventing-webhook-certs unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev unchanged
deployment "eventing-controller" successfully rolled out
service/autoscaler annotated
service/autoscaler annotated
service/activator-service annotated
service/activator-service annotated
deployment "eventing-controller" successfully rolled out
deployment "eventing-webhook" successfully rolled out
configmap/config-imc-event-dispatcher created
clusterrole.rbac.authorization.k8s.io/imc-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/imc-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/imc-controller created
serviceaccount/imc-controller created
clusterrole.rbac.authorization.k8s.io/imc-dispatcher created
service/imc-dispatcher created
serviceaccount/imc-dispatcher created
clusterrolebinding.rbac.authorization.k8s.io/imc-controller created
clusterrolebinding.rbac.authorization.k8s.io/imc-dispatcher created
customresourcedefinition.apiextensions.k8s.io/inmemorychannels.messaging.knative.dev created
deployment.apps/imc-controller created
deployment.apps/imc-dispatcher created
deployment "imc-controller" successfully rolled out
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-channel-broker-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
serviceaccount/mt-broker-filter created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
serviceaccount/mt-broker-ingress created
clusterrolebinding.rbac.authorization.k8s.io/eventing-mt-channel-broker-controller created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
deployment.apps/mt-broker-filter created
service/broker-filter created
deployment.apps/mt-broker-ingress created
service/broker-ingress created
deployment.apps/mt-broker-controller created
horizontalpodautoscaler.autoscaling/broker-ingress-hpa created
horizontalpodautoscaler.autoscaling/broker-filter-hpa created
deployment "mt-broker-controller" successfully rolled out
deployment "mt-broker-filter" successfully rolled out
+ '[' true = true ']'
+ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.18.0/serving-default-domain.yaml
job.batch/default-domain created
service/default-domain-service created
+ install_argo
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/argo
+ ./argo.sh
namespace/argo created
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/clusterworkflowtemplates.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/cronworkflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workfloweventbindings.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflowtemplates.argoproj.io created
serviceaccount/argo created
serviceaccount/argo-server created
role.rbac.authorization.k8s.io/argo-role created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-admin created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-edit created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-view created
clusterrole.rbac.authorization.k8s.io/argo-cluster-role created
clusterrole.rbac.authorization.k8s.io/argo-server-cluster-role created
rolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-server-binding created
configmap/workflow-controller-configmap created
service/argo-server created
service/workflow-controller-metrics created
deployment.apps/argo-server created
deployment.apps/workflow-controller created
configmap/workflow-controller-configmap configured
+ install_minio
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/minio
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./minio.sh
TEMPRESOURCES IS /tmp/tempresources
SD_USER_EMAIL IS admin@seldon-ey.io
namespace/minio-system created
"minio" has been added to your repositories
Release "minio" does not exist. Installing it now.
NAME: minio
LAST DEPLOYED: Wed Oct 20 12:13:45 2021
NAMESPACE: minio-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Minio can be accessed via port 9000 on the following DNS name from within your cluster:
minio.minio-system.svc.cluster.local

To access Minio from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace minio-system -l "release=minio" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace minio-system

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access Minio server on http://localhost:9000. Follow the below steps to connect to Minio server with mc client:

  1. Download the Minio mc client - https://docs.minio.io/docs/minio-client-quickstart-guide

  2. Get the ACCESS_KEY=$(kubectl get secret minio -o jsonpath="{.data.accesskey}" | base64 --decode) and the SECRET_KEY=$(kubectl get secret minio -o jsonpath="{.data.secretkey}" | base64 --decode)

  3. mc alias set minio-local http://localhost:9000 "$ACCESS_KEY" "$SECRET_KEY" --api s3v4

  4. mc ls minio-local

Alternately, you can use your browser or the Minio SDK to access the server - https://docs.minio.io/categories/17
virtualservice.networking.istio.io/minio created
+ install_EFK_and_logger
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk
+ export TEMPRESOURCES
+ ./install_efk.sh
TEMPRESOURCES IS /tmp/tempresources
Error from server (AlreadyExists): namespaces "seldon-logs" already exists
namespace seldon-logs exists
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/elastic-credentials created
secret/elastic-credentials created
Cloning into 'opendistro-build'...
remote: Enumerating objects: 7421, done.
remote: Counting objects: 100% (531/531), done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 7421 (delta 343), reused 422 (delta 266), pack-reused 6890
Receiving objects: 100% (7421/7421), 1.90 MiB | 805.00 KiB/s, done.
Resolving deltas: 100% (5084/5084), done.
Fetching origin
Note: switching to 'tags/v1.13.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at aabb00f Modify script and workflow for AMI to include ARM64  (#738)
Successfully packaged chart and saved it to: /tmp/tempresources/opendistro-build/helm/opendistro-es/opendistro-es-1.13.2.tgz
Release "elasticsearch" does not exist. Installing it now.
W1020 12:14:37.341245   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:43.646754   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:44.920126   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:57.940282   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:59.050377   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:59.050983   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
NAME: elasticsearch
LAST DEPLOYED: Wed Oct 20 12:14:34 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
Release "fluentd" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: fluentd
LAST DEPLOYED: Wed Oct 20 12:15:10 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=seldon-logs get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.
Waiting for deployment "elasticsearch-opendistro-es-kibana" rollout to finish: 0 of 1 updated replicas are available...
deployment "elasticsearch-opendistro-es-kibana" successfully rolled out
+ ./eventing_for_logs_ns.sh
broker.eventing.knative.dev/default created
knative broker created
+ kubectl apply -f /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk/kibana-virtualservice.yaml
virtualservice.networking.istio.io/kibana created
+ install_seldon_core
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/seldon-core
+ export TEMPRESOURCES
+ export SELDON_CORE_VERSION
+ export MULTITENANT
+ export EXTERNAL_PROTOCOL
+ ./install_seldon_core.sh
SELDON CORE VERSION v1.9.1
Cloning into 'seldon-core'...
remote: Enumerating objects: 130545, done.
remote: Counting objects: 100% (2898/2898), done.
remote: Compressing objects: 100% (1172/1172), done.
remote: Total 130545 (delta 1846), reused 2511 (delta 1606), pack-reused 127647
Receiving objects: 100% (130545/130545), 212.37 MiB | 824.00 KiB/s, done.
Resolving deltas: 100% (78770/78770), done.
Note: switching to '8ad2ede5ca18e321f8603f1e2a821e767af000de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

using /tmp/tempresources/seldon-core
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
gateway.networking.istio.io/seldon-gateway configured
Release "seldon-core" does not exist. Installing it now.
W1020 12:21:32.726503   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
W1020 12:21:57.693208   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
NAME: seldon-core
LAST DEPLOYED: Wed Oct 20 12:21:13 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
Waiting for deployment "seldon-controller-manager" rollout to finish: 0 of 1 updated replicas are available...
deployment "seldon-controller-manager" successfully rolled out
+ install_analytics
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/prometheus
+ export TEMPRESOURCES
+ ./seldon-core-analytics.sh
configmap/model-usage-rules created
Error from server (NotFound): deployments.apps "seldon-core-analytics-prometheus-seldon" not found
Release "seldon-core-analytics" does not exist. Installing it now.
W1020 12:28:18.796115   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:20.023979   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:49.096327   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:50.323697   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:51.355141   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:52.574403   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:53.599335   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:55.648768   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:56.670352   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:57.676505   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:58.922424   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:00.149772   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:01.379295   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:03.834611   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
W1020 12:29:22.466916   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:22.467337   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:25.947779   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.951773   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.988757   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.994807   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.995223   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:26.358782   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358910   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359018   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358798   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359349   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.767071   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:27.176581   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
NAME: seldon-core-analytics
LAST DEPLOYED: Wed Oct 20 12:28:15 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
+ install_kfserving
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/kfserving
+ export TEMPRESOURCES
+ export KFSERVING_TAG
+ ./install_kfserving.sh
TEMPRESOURCES IS /tmp/tempresources
KFSERVING_TAG v0.4.1
Cloning into 'kfserving'...
remote: Enumerating objects: 44567, done.
remote: Counting objects: 100% (1826/1826), done.
remote: Compressing objects: 100% (1192/1192), done.
remote: Total 44567 (delta 839), reused 1249 (delta 566), pack-reused 42741
Receiving objects: 100% (44567/44567), 116.21 MiB | 800.00 KiB/s, done.
Resolving deltas: 100% (17763/17763), done.
Note: switching to 'f253dd529ba25c080ca458d8dc36fd0a19bbd473'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f253dd52 update 0.4.1 yaml (#1176)
using /tmp/tempresources/kfserving
namespace/kfserving-system created
Warning: resource namespaces/kfserving-system is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/kfserving-system configured
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/inferenceservices.serving.kubeflow.org created
Warning: admissionregistration.k8s.io/v1beta1 MutatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 MutatingWebhookConfiguration
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
role.rbac.authorization.k8s.io/leader-election-role created
clusterrole.rbac.authorization.k8s.io/kfserving-manager-role created
clusterrole.rbac.authorization.k8s.io/kfserving-proxy-role created
rolebinding.rbac.authorization.k8s.io/leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-proxy-rolebinding created
configmap/inferenceservice-config created
secret/kfserving-webhook-server-secret created
service/kfserving-controller-manager-metrics-service created
service/kfserving-controller-manager-service created
service/kfserving-webhook-server-service created
statefulset.apps/kfserving-controller-manager created
Warning: admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Certificate" in version "cert-manager.io/v1alpha2"
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Issuer" in version "cert-manager.io/v1alpha2"
configmap/inferenceservice-config patched
service: kfserving-webhook-server-service
namespace: kfserving-system
secret: kfserving-webhook-server-cert
webhookDeploymentName: kfserving-controller-manager-0
webhookConfigName: inferenceservice.serving.kubeflow.org
creating certs in tmpdir /tmp/tmp.VFjc8KH97E 
Generating RSA private key, 2048 bit long modulus (2 primes)
.......................+++++
...........................................................+++++
e is 65537 (0x010001)
Generating RSA private key, 2048 bit long modulus (2 primes)
........................................................................................+++++
......................................................................+++++
e is 65537 (0x010001)
Signature ok
subject=CN = kfserving-webhook-server-service.kfserving-system.svc
Getting CA Private Key
W1020 12:32:50.683819   37974 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
secret/kfserving-webhook-server-cert created
pod "kfserving-controller-manager-0" deleted
webhook kfserving-controller-manager-0 is restarted to utilize the new secret
CA Certificate:
-----BEGIN CERTIFICATE-----
MIIDYTCCAkmgAwIBAgIUIwKbuXlVEBkLnIHYAy0VIOtbhEIwDQYJKoZIhvcNAQEL
BQAwQDE+MDwGA1UEAww1a2ZzZXJ2aW5nLXdlYmhvb2stc2VydmVyLXNlcnZpY2Uu
a2ZzZXJ2aW5nLXN5c3RlbS5zdmMwHhcNMjExMDIwMDcwMjUwWhcNMjIxMDIwMDcw
MjUwWjBAMT4wPAYDVQQDDDVrZnNlcnZpbmctd2ViaG9vay1zZXJ2ZXItc2Vydmlj
ZS5rZnNlcnZpbmctc3lzdGVtLnN2YzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKqYeLIbze8FaJMmaThqsu9gfXsBwXubosNWODeP9KkN1K0MZhPQc2uJ
5fSwW13cxRaXYnOfaT2AmYdXJZKLBKSWCPPli2rIG9sK0uSm6uR6F/wiXRxlhWHI
R2IXzvbChEczanKCj9WGqolBv2pORYToROmtKxrOmgIx80bwWMKRYARskZtXwUe2
q1OYIsjM0iTMxLgTb1sQs1fXXQ2IgGgYXsonK7FRkcfI7mN0BmcOesOnTw1FAcPO
I7D+FKVZfiQxTY8ktx7WxlszKcmh7hd0KOJC2sHfCUJf82O4h8R/ugtSeS/m1K+n
171KW4DpYccvbKDLA8KotO7nTaN5YXcCAwEAAaNTMFEwHQYDVR0OBBYEFNhFaXMQ
qRjegiNmObr9mZHh4QdtMB8GA1UdIwQYMBaAFNhFaXMQqRjegiNmObr9mZHh4Qdt
MA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAA2wU0Ei06Mrd8hW
yscVL1R0odDF5m2pAVhE2Jgig3Di2gLNaEHT0jjOVSWoDRDyxPy8I0a+KirqlWwA
5/2uQiAE60rTLugKO+xdHgkGp3j/QWK6bczlm4S2b5cD0blv+u0TFbnikbKUFRJ1
EpBuLcKWQJUOEvmgtikYeDEsyLrozu8OnxHXiO1bn2ZRPhnDHvbgNb+IeBaeq+a9
NFoN87NOiqXVTxLUt7W4JhazM8ZuOeEfQUzl7k3Wgle9aY37rviD14MMboPigA74
5OB8HTMrpvcCvvqJaszuxirSwHK+y54rKbuNiHQGbnC384viA/JY9qGD4R1kopu0
W+A9NeU=
-----END CERTIFICATE-----
Encoded CA:
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURZVENDQWttZ0F3SUJBZ0lVSXdLYnVYbFZFQmtMbklIWUF5MFZJT3RiaEVJd0RRWUpLb1pJaHZjTkFRRUwKQlFBd1FERStNRHdHQTFVRUF3dzFhMlp6WlhKMmFXNW5MWGRsWW1odmIyc3RjMlZ5ZG1WeUxYTmxjblpwWTJVdQphMlp6WlhKMmFXNW5MWE41YzNSbGJTNXpkbU13SGhjTk1qRXhNREl3TURjd01qVXdXaGNOTWpJeE1ESXdNRGN3Ck1qVXdXakJBTVQ0d1BBWURWUVFERERWclpuTmxjblpwYm1jdGQyVmlhRzl2YXkxelpYSjJaWEl0YzJWeWRtbGoKWlM1clpuTmxjblpwYm1jdGMzbHpkR1Z0TG5OMll6Q0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQwpBUW9DZ2dFQkFLcVllTEliemU4RmFKTW1hVGhxc3U5Z2ZYc0J3WHVib3NOV09EZVA5S2tOMUswTVpoUFFjMnVKCjVmU3dXMTNjeFJhWFluT2ZhVDJBbVlkWEpaS0xCS1NXQ1BQbGkycklHOXNLMHVTbTZ1UjZGL3dpWFJ4bGhXSEkKUjJJWHp2YkNoRWN6YW5LQ2o5V0dxb2xCdjJwT1JZVG9ST210S3hyT21nSXg4MGJ3V01LUllBUnNrWnRYd1VlMgpxMU9ZSXNqTTBpVE14TGdUYjFzUXMxZlhYUTJJZ0dnWVhzb25LN0ZSa2NmSTdtTjBCbWNPZXNPblR3MUZBY1BPCkk3RCtGS1ZaZmlReFRZOGt0eDdXeGxzektjbWg3aGQwS09KQzJzSGZDVUpmODJPNGg4Ui91Z3RTZVMvbTFLK24KMTcxS1c0RHBZY2N2YktETEE4S290TzduVGFONVlYY0NBd0VBQWFOVE1GRXdIUVlEVlIwT0JCWUVGTmhGYVhNUQpxUmplZ2lObU9icjltWkhoNFFkdE1COEdBMVVkSXdRWU1CYUFGTmhGYVhNUXFSamVnaU5tT2JyOW1aSGg0UWR0Ck1BOEdBMVVkRXdFQi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBMndVMEVpMDZNcmQ4aFcKeXNjVkwxUjBvZERGNW0ycEFWaEUySmdpZzNEaTJnTE5hRUhUMGpqT1ZTV29EUkR5eFB5OEkwYStLaXJxbFd3QQo1LzJ1UWlBRTYwclRMdWdLTyt4ZEhna0dwM2ovUVdLNmJjemxtNFMyYjVjRDBibHYrdTBURmJuaWtiS1VGUkoxCkVwQnVMY0tXUUpVT0V2bWd0aWtZZURFc3lMcm96dThPbnhIWGlPMWJuMlpSUGhuREh2YmdOYitJZUJhZXErYTkKTkZvTjg3Tk9pcVhWVHhMVXQ3VzRKaGF6TThadU9lRWZRVXpsN2szV2dsZTlhWTM3cnZpRDE0TU1ib1BpZ0E3NAo1T0I4SFRNcnB2Y0N2dnFKYXN6dXhpclN3SEsreTU0cktidU5pSFFHYm5DMzg0dmlBL0pZOXFHRDRSMWtvcHUwClcrQTlOZVU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K 

patching ca bundle for mutating webhook configuration...
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
patching ca bundle for validating webhook configuration...
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
+ configure_namespaces
+ kubectl create namespace seldon
namespace/seldon created
+ kubectl label ns seldon seldon.restricted=false --overwrite=true
namespace/seldon labeled
+ kubectl label ns seldon serving.kubeflow.org/inferenceservice=enabled --overwrite=true
namespace/seldon labeled
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/configure-batch-on-ns
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./batch-sa-for-ns.sh
TEMPRESOURCES IS /tmp/tempresources
role.rbac.authorization.k8s.io/workflow created
serviceaccount/workflow created
rolebinding.rbac.authorization.k8s.io/workflow created
secret/seldon-job-secret created
Error from server (NotFound): namespaces "kubeflow" not found
secret/seldon-job-secret configured
configured for minio in minio-system
+ install_postgres
+ '[' true = true ']'
+ echo 'Installing postgres...'
Installing postgres...
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/postgres
+ export TEMPRESOURCES
+ export STARTUP_DIR
+ POSTGRES_MANIFEST=minimal-postgres-manifest.yaml
+ ./install_postgres.sh
Installing zalando postgres operator and a db instance if required
Cloning into 'postgres-operator'...
remote: Enumerating objects: 22250, done.
remote: Counting objects: 100% (2142/2142), done.
remote: Compressing objects: 100% (964/964), done.
remote: Total 22250 (delta 1504), reused 1700 (delta 1145), pack-reused 20108
Receiving objects: 100% (22250/22250), 8.71 MiB | 915.00 KiB/s, done.
Resolving deltas: 100% (15803/15803), done.
Note: switching to 'v1.6.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c18241f1 Bump v1.6.2 (#1433)
namespace/postgres created
Release "postgres-operator" does not exist. Installing it now.
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: postgres-operator
LAST DEPLOYED: Wed Oct 20 12:34:07 2021
NAMESPACE: postgres
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that postgres-operator has started, run:

  kubectl --namespace=postgres get pods -l "app.kubernetes.io/name=postgres-operator"
postgresql.acid.zalan.do/seldon-metadata-storage created
The postgres secret has been created by the operator...
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/metadata-postgres created
+ install_keycloak_auth
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/keycloak
+ ./install_keycloak.sh
Error from server (AlreadyExists): namespaces "seldon-system" already exists
secret/realm-secret created
Release "keycloak" does not exist. Installing it now.
NAME: keycloak
LAST DEPLOYED: Wed Oct 20 12:35:16 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
NOTES:
Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  keycloak-http.seldon-system.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

  export POD_NAME=$(kubectl get pods --namespace seldon-system -l app.kubernetes.io/instance=keycloak -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use Keycloak"
  kubectl port-forward --namespace seldon-system $POD_NAME 8080

Login with the following credentials:
Username: "admin@seldon-ey.io"

To retrieve the initial user password run:
kubectl get secret --namespace seldon-system keycloak-http -o jsonpath="{.data.password}" | base64 --decode; echo
virtualservice.networking.istio.io/keycloak created
Waiting for 1 pods to be ready...
statefulset rolling update complete 1 pods at revision keycloak-5d9666fb66...
Creating default keycloak user
 * Default user created
Creating API auth client
 * API client created
 * Keycloak setup completed
[sepoy@xps seldon-deploy-install]$ ./sd-setup/sd-install-default
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/git-creds configured
namespace/argocd configured
Error from server (AlreadyExists): namespaces "seldon-system" already exists
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/request-logger-auth configured
./sd-setup/sd-install-default: line 80: EXTERNAL_HOST: unbound variable
[sepoy@xps seldon-deploy-install]$ ./sd-setup/show-seldon-deploy-url
http://a38fbee579f06403bb22116c69dcb22d-972759690.us-east-2.elb.amazonaws.com/seldon-deploy/
[sepoy@xps seldon-deploy-install]$ ./prerequisites-setup/default-setup.sh
+++ dirname ./prerequisites-setup/default-setup.sh
++ cd ./prerequisites-setup
++ pwd
+ STARTUP_DIR=/home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ SELDON_CORE_DIR=
+ KFSERVING_DIR=
+ SELDON_CORE_VERSION=v1.9.1
+ KFSERVING_TAG=v0.4.1
+ ENABLE_KNATIVE_XIP=true
+ TEMPRESOURCES=/tmp/tempresources
+ SDCONFIG_FILE=/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
+ source /home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
++ GIT_USER=fourtimes
++ GIT_TOKEN=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
++ GIT_EMAIL=jjino@protonmail.com
++ ENABLE_GIT_SSH_CREDS=false
++ SD_USER_EMAIL=admin@seldon-ey.io
++ SD_PASSWORD=ChangeMe@123
++ XTERNAL_HOST=
++ EXTERNAL_PROTOCOL=http
++ KFSERVING_PROTOCOL=http
++ MULTITENANT=false
++ ENABLE_APP_AUTH=true
++ VIRTUALSERVICE_CREATE=true
++ ENABLE_METADATA_POSTGRES=true
++ ENABLE_OPA=false
++ ENABLE_PROJECT_BASED_AUTH=false
++ ENABLE_AUDIT=true
+ ENABLE_METADATA_POSTGRES=true
+ check_creds
+ ((  18 < 8  ))
+ ((  12 < 8  ))
+ setup_tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/clean
removed /tmp/tempresources
+ mkdir -p /tmp/tempresources
+ create_istio
+ cd /tmp/tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/istio/install_istio_new.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   102  100   102    0     0     70      0  0:00:01  0:00:01 --:--:--    70
100  4549  100  4549    0     0   2086      0  0:00:02  0:00:02 --:--:--     0

Downloading istio-1.7.3 from https://github.com/istio/istio/releases/download/1.7.3/istio-1.7.3-linux-amd64.tar.gz ...

Istio 1.7.3 Download Complete!

Istio has been successfully downloaded into the istio-1.7.3 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /tmp/tempresources/istio-1.7.3/bin directory to your environment path variable with:
	 export PATH="$PATH:/tmp/tempresources/istio-1.7.3/bin"

Begin the Istio pre-installation check by running:
	 istioctl x precheck 

Need more information? Visit https://istio.io/latest/docs/setup/install/ 
Installing istio
✔ Istio core installed                                                                                                                                                                        
✔ Istiod installed                                                                                                                                                                            
✔ Addons installed                                                                                                                                                                            
✔ Ingress gateways installed                                                                                                                                                                  
✔ Installation complete                                                                                                                                                                       istio & gateway setup completed
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ wait_istio_ready
+ kubectl rollout status -n istio-system deployment.v1.apps/istio-ingressgateway
deployment "istio-ingressgateway" successfully rolled out
+ configure_https
+ '[' http = https ']'
+ create_knative
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/knative
+ ./install_knative.sh
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev created
namespace/knative-serving created
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-serving-core created
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding created
serviceaccount/controller created
clusterrole.rbac.authorization.k8s.io/knative-serving-admin created
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy created
configmap/config-autoscaler created
configmap/config-defaults created
configmap/config-deployment created
configmap/config-domain created
configmap/config-features created
configmap/config-gc created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-network created
configmap/config-observability created
configmap/config-tracing created
horizontalpodautoscaler.autoscaling/activator created
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb created
deployment.apps/activator created
service/activator-service created
deployment.apps/autoscaler created
service/autoscaler created
deployment.apps/controller created
service/controller created
deployment.apps/webhook created
service/webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev created
secret/webhook-certs created
clusterrole.rbac.authorization.k8s.io/knative-serving-istio created
gateway.networking.istio.io/knative-ingress-gateway created
gateway.networking.istio.io/cluster-local-gateway created
gateway.networking.istio.io/knative-local-gateway created
service/knative-local-gateway created
peerauthentication.security.istio.io/webhook created
peerauthentication.security.istio.io/istio-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev created
secret/istio-webhook-certs created
configmap/config-istio created
deployment.apps/networking-istio created
deployment.apps/istio-webhook created
service/istio-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev created
namespace/knative-eventing created
serviceaccount/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator created
serviceaccount/pingsource-mt-adapter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
serviceaccount/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding created
configmap/config-br-default-channel created
configmap/config-br-defaults created
configmap/default-ch-webhook created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-observability created
configmap/config-tracing created
deployment.apps/eventing-controller created
deployment.apps/pingsource-mt-adapter created
deployment.apps/eventing-webhook created
service/eventing-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver created
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter created
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress created
clusterrole.rbac.authorization.k8s.io/eventing-config-reader created
clusterrole.rbac.authorization.k8s.io/channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
clusterrole.rbac.authorization.k8s.io/podspecable-binding created
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding created
clusterrole.rbac.authorization.k8s.io/source-observer created
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer created
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev created
secret/eventing-webhook-certs created
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev created
Sleep and run again - needed for Kind install as not all CRDs get installed sometimes
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
namespace/knative-serving unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-core unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding unchanged
serviceaccount/controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-admin configured
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy unchanged
configmap/config-autoscaler unchanged
configmap/config-defaults unchanged
configmap/config-deployment unchanged
configmap/config-domain unchanged
configmap/config-features unchanged
configmap/config-gc unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-network unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
horizontalpodautoscaler.autoscaling/activator unchanged
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb configured
deployment.apps/activator configured
service/activator-service unchanged
deployment.apps/autoscaler unchanged
service/autoscaler unchanged
deployment.apps/controller configured
service/controller unchanged
deployment.apps/webhook unchanged
service/webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev unchanged
secret/webhook-certs unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-istio unchanged
gateway.networking.istio.io/knative-ingress-gateway unchanged
gateway.networking.istio.io/cluster-local-gateway unchanged
gateway.networking.istio.io/knative-local-gateway unchanged
service/knative-local-gateway unchanged
peerauthentication.security.istio.io/webhook unchanged
peerauthentication.security.istio.io/istio-webhook unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev unchanged
secret/istio-webhook-certs unchanged
configmap/config-istio unchanged
deployment.apps/networking-istio unchanged
deployment.apps/istio-webhook unchanged
service/istio-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
namespace/knative-eventing unchanged
serviceaccount/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator unchanged
serviceaccount/pingsource-mt-adapter unchanged
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
serviceaccount/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding unchanged
configmap/config-br-default-channel unchanged
configmap/config-br-defaults unchanged
configmap/default-ch-webhook unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
deployment.apps/eventing-controller unchanged
deployment.apps/pingsource-mt-adapter configured
deployment.apps/eventing-webhook unchanged
service/eventing-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver configured
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress unchanged
clusterrole.rbac.authorization.k8s.io/eventing-config-reader unchanged
clusterrole.rbac.authorization.k8s.io/channelable-manipulator configured
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
clusterrole.rbac.authorization.k8s.io/podspecable-binding configured
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding unchanged
clusterrole.rbac.authorization.k8s.io/source-observer configured
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev unchanged
secret/eventing-webhook-certs unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev unchanged
deployment "eventing-controller" successfully rolled out
service/autoscaler annotated
service/autoscaler annotated
service/activator-service annotated
service/activator-service annotated
deployment "eventing-controller" successfully rolled out
deployment "eventing-webhook" successfully rolled out
configmap/config-imc-event-dispatcher created
clusterrole.rbac.authorization.k8s.io/imc-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/imc-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/imc-controller created
serviceaccount/imc-controller created
clusterrole.rbac.authorization.k8s.io/imc-dispatcher created
service/imc-dispatcher created
serviceaccount/imc-dispatcher created
clusterrolebinding.rbac.authorization.k8s.io/imc-controller created
clusterrolebinding.rbac.authorization.k8s.io/imc-dispatcher created
customresourcedefinition.apiextensions.k8s.io/inmemorychannels.messaging.knative.dev created
deployment.apps/imc-controller created
deployment.apps/imc-dispatcher created
deployment "imc-controller" successfully rolled out
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-channel-broker-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
serviceaccount/mt-broker-filter created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
serviceaccount/mt-broker-ingress created
clusterrolebinding.rbac.authorization.k8s.io/eventing-mt-channel-broker-controller created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
deployment.apps/mt-broker-filter created
service/broker-filter created
deployment.apps/mt-broker-ingress created
service/broker-ingress created
deployment.apps/mt-broker-controller created
horizontalpodautoscaler.autoscaling/broker-ingress-hpa created
horizontalpodautoscaler.autoscaling/broker-filter-hpa created
deployment "mt-broker-controller" successfully rolled out
deployment "mt-broker-filter" successfully rolled out
+ '[' true = true ']'
+ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.18.0/serving-default-domain.yaml
job.batch/default-domain created
service/default-domain-service created
+ install_argo
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/argo
+ ./argo.sh
namespace/argo created
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/clusterworkflowtemplates.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/cronworkflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workfloweventbindings.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflowtemplates.argoproj.io created
serviceaccount/argo created
serviceaccount/argo-server created
role.rbac.authorization.k8s.io/argo-role created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-admin created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-edit created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-view created
clusterrole.rbac.authorization.k8s.io/argo-cluster-role created
clusterrole.rbac.authorization.k8s.io/argo-server-cluster-role created
rolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-server-binding created
configmap/workflow-controller-configmap created
service/argo-server created
service/workflow-controller-metrics created
deployment.apps/argo-server created
deployment.apps/workflow-controller created
configmap/workflow-controller-configmap configured
+ install_minio
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/minio
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./minio.sh
TEMPRESOURCES IS /tmp/tempresources
SD_USER_EMAIL IS admin@seldon-ey.io
namespace/minio-system created
"minio" has been added to your repositories
Release "minio" does not exist. Installing it now.
NAME: minio
LAST DEPLOYED: Wed Oct 20 12:13:45 2021
NAMESPACE: minio-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Minio can be accessed via port 9000 on the following DNS name from within your cluster:
minio.minio-system.svc.cluster.local

To access Minio from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace minio-system -l "release=minio" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace minio-system

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access Minio server on http://localhost:9000. Follow the below steps to connect to Minio server with mc client:

  1. Download the Minio mc client - https://docs.minio.io/docs/minio-client-quickstart-guide

  2. Get the ACCESS_KEY=$(kubectl get secret minio -o jsonpath="{.data.accesskey}" | base64 --decode) and the SECRET_KEY=$(kubectl get secret minio -o jsonpath="{.data.secretkey}" | base64 --decode)

  3. mc alias set minio-local http://localhost:9000 "$ACCESS_KEY" "$SECRET_KEY" --api s3v4

  4. mc ls minio-local

Alternately, you can use your browser or the Minio SDK to access the server - https://docs.minio.io/categories/17
virtualservice.networking.istio.io/minio created
+ install_EFK_and_logger
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk
+ export TEMPRESOURCES
+ ./install_efk.sh
TEMPRESOURCES IS /tmp/tempresources
Error from server (AlreadyExists): namespaces "seldon-logs" already exists
namespace seldon-logs exists
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/elastic-credentials created
secret/elastic-credentials created
Cloning into 'opendistro-build'...
remote: Enumerating objects: 7421, done.
remote: Counting objects: 100% (531/531), done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 7421 (delta 343), reused 422 (delta 266), pack-reused 6890
Receiving objects: 100% (7421/7421), 1.90 MiB | 805.00 KiB/s, done.
Resolving deltas: 100% (5084/5084), done.
Fetching origin
Note: switching to 'tags/v1.13.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at aabb00f Modify script and workflow for AMI to include ARM64  (#738)
Successfully packaged chart and saved it to: /tmp/tempresources/opendistro-build/helm/opendistro-es/opendistro-es-1.13.2.tgz
Release "elasticsearch" does not exist. Installing it now.
W1020 12:14:37.341245   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:43.646754   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:44.920126   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:57.940282   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:59.050377   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:59.050983   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
NAME: elasticsearch
LAST DEPLOYED: Wed Oct 20 12:14:34 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
Release "fluentd" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: fluentd
LAST DEPLOYED: Wed Oct 20 12:15:10 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=seldon-logs get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.
Waiting for deployment "elasticsearch-opendistro-es-kibana" rollout to finish: 0 of 1 updated replicas are available...
deployment "elasticsearch-opendistro-es-kibana" successfully rolled out
+ ./eventing_for_logs_ns.sh
broker.eventing.knative.dev/default created
knative broker created
+ kubectl apply -f /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk/kibana-virtualservice.yaml
virtualservice.networking.istio.io/kibana created
+ install_seldon_core
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/seldon-core
+ export TEMPRESOURCES
+ export SELDON_CORE_VERSION
+ export MULTITENANT
+ export EXTERNAL_PROTOCOL
+ ./install_seldon_core.sh
SELDON CORE VERSION v1.9.1
Cloning into 'seldon-core'...
remote: Enumerating objects: 130545, done.
remote: Counting objects: 100% (2898/2898), done.
remote: Compressing objects: 100% (1172/1172), done.
remote: Total 130545 (delta 1846), reused 2511 (delta 1606), pack-reused 127647
Receiving objects: 100% (130545/130545), 212.37 MiB | 824.00 KiB/s, done.
Resolving deltas: 100% (78770/78770), done.
Note: switching to '8ad2ede5ca18e321f8603f1e2a821e767af000de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

using /tmp/tempresources/seldon-core
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
gateway.networking.istio.io/seldon-gateway configured
Release "seldon-core" does not exist. Installing it now.
W1020 12:21:32.726503   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
W1020 12:21:57.693208   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
NAME: seldon-core
LAST DEPLOYED: Wed Oct 20 12:21:13 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
Waiting for deployment "seldon-controller-manager" rollout to finish: 0 of 1 updated replicas are available...
deployment "seldon-controller-manager" successfully rolled out
+ install_analytics
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/prometheus
+ export TEMPRESOURCES
+ ./seldon-core-analytics.sh
configmap/model-usage-rules created
Error from server (NotFound): deployments.apps "seldon-core-analytics-prometheus-seldon" not found
Release "seldon-core-analytics" does not exist. Installing it now.
W1020 12:28:18.796115   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:20.023979   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:49.096327   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:50.323697   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:51.355141   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:52.574403   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:53.599335   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:55.648768   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:56.670352   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:57.676505   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:58.922424   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:00.149772   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:01.379295   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:03.834611   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
W1020 12:29:22.466916   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:22.467337   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:25.947779   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.951773   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.988757   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.994807   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.995223   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:26.358782   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358910   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359018   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358798   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359349   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.767071   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:27.176581   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
NAME: seldon-core-analytics
LAST DEPLOYED: Wed Oct 20 12:28:15 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
+ install_kfserving
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/kfserving
+ export TEMPRESOURCES
+ export KFSERVING_TAG
+ ./install_kfserving.sh
TEMPRESOURCES IS /tmp/tempresources
KFSERVING_TAG v0.4.1
Cloning into 'kfserving'...
remote: Enumerating objects: 44567, done.
remote: Counting objects: 100% (1826/1826), done.
remote: Compressing objects: 100% (1192/1192), done.
remote: Total 44567 (delta 839), reused 1249 (delta 566), pack-reused 42741
Receiving objects: 100% (44567/44567), 116.21 MiB | 800.00 KiB/s, done.
Resolving deltas: 100% (17763/17763), done.
Note: switching to 'f253dd529ba25c080ca458d8dc36fd0a19bbd473'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f253dd52 update 0.4.1 yaml (#1176)
using /tmp/tempresources/kfserving
namespace/kfserving-system created
Warning: resource namespaces/kfserving-system is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/kfserving-system configured
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/inferenceservices.serving.kubeflow.org created
Warning: admissionregistration.k8s.io/v1beta1 MutatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 MutatingWebhookConfiguration
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
role.rbac.authorization.k8s.io/leader-election-role created
clusterrole.rbac.authorization.k8s.io/kfserving-manager-role created
clusterrole.rbac.authorization.k8s.io/kfserving-proxy-role created
rolebinding.rbac.authorization.k8s.io/leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-proxy-rolebinding created
configmap/inferenceservice-config created
secret/kfserving-webhook-server-secret created
service/kfserving-controller-manager-metrics-service created
service/kfserving-controller-manager-service created
service/kfserving-webhook-server-service created
statefulset.apps/kfserving-controller-manager created
Warning: admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Certificate" in version "cert-manager.io/v1alpha2"
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Issuer" in version "cert-manager.io/v1alpha2"
configmap/inferenceservice-config patched
service: kfserving-webhook-server-service
namespace: kfserving-system
secret: kfserving-webhook-server-cert
webhookDeploymentName: kfserving-controller-manager-0
webhookConfigName: inferenceservice.serving.kubeflow.org
creating certs in tmpdir /tmp/tmp.VFjc8KH97E 
Generating RSA private key, 2048 bit long modulus (2 primes)
.......................+++++
...........................................................+++++
e is 65537 (0x010001)
Generating RSA private key, 2048 bit long modulus (2 primes)
........................................................................................+++++
......................................................................+++++
e is 65537 (0x010001)
Signature ok
subject=CN = kfserving-webhook-server-service.kfserving-system.svc
Getting CA Private Key
W1020 12:32:50.683819   37974 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
secret/kfserving-webhook-server-cert created
pod "kfserving-controller-manager-0" deleted
webhook kfserving-controller-manager-0 is restarted to utilize the new secret
CA Certificate:
-----BEGIN CERTIFICATE-----
MIIDYTCCAkmgAwIBAgIUIwKbuXlVEBkLnIHYAy0VIOtbhEIwDQYJKoZIhvcNAQEL
BQAwQDE+MDwGA1UEAww1a2ZzZXJ2aW5nLXdlYmhvb2stc2VydmVyLXNlcnZpY2Uu
a2ZzZXJ2aW5nLXN5c3RlbS5zdmMwHhcNMjExMDIwMDcwMjUwWhcNMjIxMDIwMDcw
MjUwWjBAMT4wPAYDVQQDDDVrZnNlcnZpbmctd2ViaG9vay1zZXJ2ZXItc2Vydmlj
ZS5rZnNlcnZpbmctc3lzdGVtLnN2YzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKqYeLIbze8FaJMmaThqsu9gfXsBwXubosNWODeP9KkN1K0MZhPQc2uJ
5fSwW13cxRaXYnOfaT2AmYdXJZKLBKSWCPPli2rIG9sK0uSm6uR6F/wiXRxlhWHI
R2IXzvbChEczanKCj9WGqolBv2pORYToROmtKxrOmgIx80bwWMKRYARskZtXwUe2
q1OYIsjM0iTMxLgTb1sQs1fXXQ2IgGgYXsonK7FRkcfI7mN0BmcOesOnTw1FAcPO
I7D+FKVZfiQxTY8ktx7WxlszKcmh7hd0KOJC2sHfCUJf82O4h8R/ugtSeS/m1K+n
171KW4DpYccvbKDLA8KotO7nTaN5YXcCAwEAAaNTMFEwHQYDVR0OBBYEFNhFaXMQ
qRjegiNmObr9mZHh4QdtMB8GA1UdIwQYMBaAFNhFaXMQqRjegiNmObr9mZHh4Qdt
MA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAA2wU0Ei06Mrd8hW
yscVL1R0odDF5m2pAVhE2Jgig3Di2gLNaEHT0jjOVSWoDRDyxPy8I0a+KirqlWwA
5/2uQiAE60rTLugKO+xdHgkGp3j/QWK6bczlm4S2b5cD0blv+u0TFbnikbKUFRJ1
EpBuLcKWQJUOEvmgtikYeDEsyLrozu8OnxHXiO1bn2ZRPhnDHvbgNb+IeBaeq+a9
NFoN87NOiqXVTxLUt7W4JhazM8ZuOeEfQUzl7k3Wgle9aY37rviD14MMboPigA74
5OB8HTMrpvcCvvqJaszuxirSwHK+y54rKbuNiHQGbnC384viA/JY9qGD4R1kopu0
W+A9NeU=
-----END CERTIFICATE-----
Encoded CA:
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURZVENDQWttZ0F3SUJBZ0lVSXdLYnVYbFZFQmtMbklIWUF5MFZJT3RiaEVJd0RRWUpLb1pJaHZjTkFRRUwKQlFBd1FERStNRHdHQTFVRUF3dzFhMlp6WlhKMmFXNW5MWGRsWW1odmIyc3RjMlZ5ZG1WeUxYTmxjblpwWTJVdQphMlp6WlhKMmFXNW5MWE41YzNSbGJTNXpkbU13SGhjTk1qRXhNREl3TURjd01qVXdXaGNOTWpJeE1ESXdNRGN3Ck1qVXdXakJBTVQ0d1BBWURWUVFERERWclpuTmxjblpwYm1jdGQyVmlhRzl2YXkxelpYSjJaWEl0YzJWeWRtbGoKWlM1clpuTmxjblpwYm1jdGMzbHpkR1Z0TG5OMll6Q0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQwpBUW9DZ2dFQkFLcVllTEliemU4RmFKTW1hVGhxc3U5Z2ZYc0J3WHVib3NOV09EZVA5S2tOMUswTVpoUFFjMnVKCjVmU3dXMTNjeFJhWFluT2ZhVDJBbVlkWEpaS0xCS1NXQ1BQbGkycklHOXNLMHVTbTZ1UjZGL3dpWFJ4bGhXSEkKUjJJWHp2YkNoRWN6YW5LQ2o5V0dxb2xCdjJwT1JZVG9ST210S3hyT21nSXg4MGJ3V01LUllBUnNrWnRYd1VlMgpxMU9ZSXNqTTBpVE14TGdUYjFzUXMxZlhYUTJJZ0dnWVhzb25LN0ZSa2NmSTdtTjBCbWNPZXNPblR3MUZBY1BPCkk3RCtGS1ZaZmlReFRZOGt0eDdXeGxzektjbWg3aGQwS09KQzJzSGZDVUpmODJPNGg4Ui91Z3RTZVMvbTFLK24KMTcxS1c0RHBZY2N2YktETEE4S290TzduVGFONVlYY0NBd0VBQWFOVE1GRXdIUVlEVlIwT0JCWUVGTmhGYVhNUQpxUmplZ2lObU9icjltWkhoNFFkdE1COEdBMVVkSXdRWU1CYUFGTmhGYVhNUXFSamVnaU5tT2JyOW1aSGg0UWR0Ck1BOEdBMVVkRXdFQi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBMndVMEVpMDZNcmQ4aFcKeXNjVkwxUjBvZERGNW0ycEFWaEUySmdpZzNEaTJnTE5hRUhUMGpqT1ZTV29EUkR5eFB5OEkwYStLaXJxbFd3QQo1LzJ1UWlBRTYwclRMdWdLTyt4ZEhna0dwM2ovUVdLNmJjemxtNFMyYjVjRDBibHYrdTBURmJuaWtiS1VGUkoxCkVwQnVMY0tXUUpVT0V2bWd0aWtZZURFc3lMcm96dThPbnhIWGlPMWJuMlpSUGhuREh2YmdOYitJZUJhZXErYTkKTkZvTjg3Tk9pcVhWVHhMVXQ3VzRKaGF6TThadU9lRWZRVXpsN2szV2dsZTlhWTM3cnZpRDE0TU1ib1BpZ0E3NAo1T0I4SFRNcnB2Y0N2dnFKYXN6dXhpclN3SEsreTU0cktidU5pSFFHYm5DMzg0dmlBL0pZOXFHRDRSMWtvcHUwClcrQTlOZVU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K 

patching ca bundle for mutating webhook configuration...
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
patching ca bundle for validating webhook configuration...
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
+ configure_namespaces
+ kubectl create namespace seldon
namespace/seldon created
+ kubectl label ns seldon seldon.restricted=false --overwrite=true
namespace/seldon labeled
+ kubectl label ns seldon serving.kubeflow.org/inferenceservice=enabled --overwrite=true
namespace/seldon labeled
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/configure-batch-on-ns
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./batch-sa-for-ns.sh
TEMPRESOURCES IS /tmp/tempresources
role.rbac.authorization.k8s.io/workflow created
serviceaccount/workflow created
rolebinding.rbac.authorization.k8s.io/workflow created
secret/seldon-job-secret created
Error from server (NotFound): namespaces "kubeflow" not found
secret/seldon-job-secret configured
configured for minio in minio-system
+ install_postgres
+ '[' true = true ']'
+ echo 'Installing postgres...'
Installing postgres...
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/postgres
+ export TEMPRESOURCES
+ export STARTUP_DIR
+ POSTGRES_MANIFEST=minimal-postgres-manifest.yaml
+ ./install_postgres.sh
Installing zalando postgres operator and a db instance if required
Cloning into 'postgres-operator'...
remote: Enumerating objects: 22250, done.
remote: Counting objects: 100% (2142/2142), done.
remote: Compressing objects: 100% (964/964), done.
remote: Total 22250 (delta 1504), reused 1700 (delta 1145), pack-reused 20108
Receiving objects: 100% (22250/22250), 8.71 MiB | 915.00 KiB/s, done.
Resolving deltas: 100% (15803/15803), done.
Note: switching to 'v1.6.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c18241f1 Bump v1.6.2 (#1433)
namespace/postgres created
Release "postgres-operator" does not exist. Installing it now.
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: postgres-operator
LAST DEPLOYED: Wed Oct 20 12:34:07 2021
NAMESPACE: postgres
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that postgres-operator has started, run:

  kubectl --namespace=postgres get pods -l "app.kubernetes.io/name=postgres-operator"
postgresql.acid.zalan.do/seldon-metadata-storage created
The postgres secret has been created by the operator...
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/metadata-postgres created
+ install_keycloak_auth
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/keycloak
+ ./install_keycloak.sh
Error from server (AlreadyExists): namespaces "seldon-system" already exists
secret/realm-secret created
Release "keycloak" does not exist. Installing it now.
NAME: keycloak
LAST DEPLOYED: Wed Oct 20 12:35:16 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
NOTES:
Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  keycloak-http.seldon-system.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

  export POD_NAME=$(kubectl get pods --namespace seldon-system -l app.kubernetes.io/instance=keycloak -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use Keycloak"
  kubectl port-forward --namespace seldon-system $POD_NAME 8080

Login with the following credentials:
Username: "admin@seldon-ey.io"

To retrieve the initial user password run:
kubectl get secret --namespace seldon-system keycloak-http -o jsonpath="{.data.password}" | base64 --decode; echo
virtualservice.networking.istio.io/keycloak created
Waiting for 1 pods to be ready...
statefulset rolling update complete 1 pods at revision keycloak-5d9666fb66...
Creating default keycloak user
 * Default user created
Creating API auth client
 * API client created
 * Keycloak setup completed
[sepoy@xps seldon-deploy-install]$ ./sd-setup/sd-install-default
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/git-creds configured
namespace/argocd configured
Error from server (AlreadyExists): namespaces "seldon-system" already exists
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/request-logger-auth configured
./sd-setup/sd-install-default: line 80: EXTERNAL_HOST: unbound variable
[sepoy@xps seldon-deploy-install]$ ./sd-setup/show-seldon-deploy-url
http://a38fbee579f06403bb22116c69dcb22d-972759690.us-east-2.elb.amazonaws.com/seldon-deploy/
times
++ GIT_TOKEN=xxxxxxxx
++ GIT_EMAIL=jjino@xxxxx.com
++ ENABLE_GIT_SSH_CREDS=false
++ SD_USER_EMAIL=admin@seldon-ey.io
++ SD_PASSWORD=ChangeMe@123
++ XTERNAL_HOST=
++ EXTERNAL_PROTOCOL=http
++ KFSERVING_PROTOCOL=http
++ MULTITENANT=false
++ ENABLE_APP_AUTH=true
++ VIRTUALSERVICE_CREATE=true
++ ENABLE_METADATA_POSTGRES=true
++ ENABLE_OPA=false
++ ENABLE_PROJECT_BASED_AUTH=false
++ ENABLE_AUDIT=true
+ ENABLE_METADATA_POSTGRES=true
+ check_creds
+ ((  18 < 8  ))
+ ((  12 < 8  ))
+ setup_tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/clean
removed /tmp/tempresources
+ mkdir -p /tmp/tempresources
+ create_istio
+ cd /tmp/tempresources
+ /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/istio/install_istio_new.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   102  100   102    0     0     70      0  0:00:01  0:00:01 --:--:--    70
100  4549  100  4549    0     0   2086      0  0:00:02  0:00:02 --:--:--     0

Downloading istio-1.7.3 from https://github.com/istio/istio/releases/download/1.7.3/istio-1.7.3-linux-amd64.tar.gz ...

Istio 1.7.3 Download Complete!

Istio has been successfully downloaded into the istio-1.7.3 folder on your system.

Next Steps:
See https://istio.io/latest/docs/setup/install/ to add Istio to your Kubernetes cluster.

To configure the istioctl client tool for your workstation,
add the /tmp/tempresources/istio-1.7.3/bin directory to your environment path variable with:
	 export PATH="$PATH:/tmp/tempresources/istio-1.7.3/bin"

Begin the Istio pre-installation check by running:
	 istioctl x precheck 

Need more information? Visit https://istio.io/latest/docs/setup/install/ 
Installing istio
✔ Istio core installed                                                                                                                                                                        
✔ Istiod installed                                                                                                                                                                            
✔ Addons installed                                                                                                                                                                            
✔ Ingress gateways installed                                                                                                                                                                  
✔ Installation complete                                                                                                                                                                       istio & gateway setup completed
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup
+ wait_istio_ready
+ kubectl rollout status -n istio-system deployment.v1.apps/istio-ingressgateway
deployment "istio-ingressgateway" successfully rolled out
+ configure_https
+ '[' http = https ']'
+ create_knative
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/knative
+ ./install_knative.sh
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev created
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev created
namespace/knative-serving created
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-serving-core created
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding created
serviceaccount/controller created
clusterrole.rbac.authorization.k8s.io/knative-serving-admin created
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin created
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy created
configmap/config-autoscaler created
configmap/config-defaults created
configmap/config-deployment created
configmap/config-domain created
configmap/config-features created
configmap/config-gc created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-network created
configmap/config-observability created
configmap/config-tracing created
horizontalpodautoscaler.autoscaling/activator created
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb created
deployment.apps/activator created
service/activator-service created
deployment.apps/autoscaler created
service/autoscaler created
deployment.apps/controller created
service/controller created
deployment.apps/webhook created
service/webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev created
secret/webhook-certs created
clusterrole.rbac.authorization.k8s.io/knative-serving-istio created
gateway.networking.istio.io/knative-ingress-gateway created
gateway.networking.istio.io/cluster-local-gateway created
gateway.networking.istio.io/knative-local-gateway created
service/knative-local-gateway created
peerauthentication.security.istio.io/webhook created
peerauthentication.security.istio.io/istio-webhook created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev created
secret/istio-webhook-certs created
configmap/config-istio created
deployment.apps/networking-istio created
deployment.apps/istio-webhook created
service/istio-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev created
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev created
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev created
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev created
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev created
namespace/knative-eventing created
serviceaccount/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller created
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator created
serviceaccount/pingsource-mt-adapter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
serviceaccount/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver created
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding created
configmap/config-br-default-channel created
configmap/config-br-defaults created
configmap/default-ch-webhook created
configmap/config-leader-election created
configmap/config-logging created
configmap/config-observability created
configmap/config-tracing created
deployment.apps/eventing-controller created
deployment.apps/pingsource-mt-adapter created
deployment.apps/eventing-webhook created
service/eventing-webhook created
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver created
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter created
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress created
clusterrole.rbac.authorization.k8s.io/eventing-config-reader created
clusterrole.rbac.authorization.k8s.io/channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit created
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view created
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter created
clusterrole.rbac.authorization.k8s.io/podspecable-binding created
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding created
clusterrole.rbac.authorization.k8s.io/source-observer created
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer created
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook created
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev created
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev created
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev created
secret/eventing-webhook-certs created
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev created
Sleep and run again - needed for Kind install as not all CRDs get installed sometimes
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
namespace/knative-serving unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-core unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-podspecable-binding unchanged
serviceaccount/controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-admin configured
clusterrolebinding.rbac.authorization.k8s.io/knative-serving-controller-admin unchanged
customresourcedefinition.apiextensions.k8s.io/images.caching.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/certificates.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/configurations.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/ingresses.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/metrics.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/podautoscalers.autoscaling.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/revisions.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/routes.serving.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/serverlessservices.networking.internal.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/services.serving.knative.dev unchanged
image.caching.internal.knative.dev/queue-proxy unchanged
configmap/config-autoscaler unchanged
configmap/config-defaults unchanged
configmap/config-deployment unchanged
configmap/config-domain unchanged
configmap/config-features unchanged
configmap/config-gc unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-network unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
horizontalpodautoscaler.autoscaling/activator unchanged
Warning: policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
poddisruptionbudget.policy/activator-pdb configured
deployment.apps/activator configured
service/activator-service unchanged
deployment.apps/autoscaler unchanged
service/autoscaler unchanged
deployment.apps/controller configured
service/controller unchanged
deployment.apps/webhook unchanged
service/webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.serving.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.serving.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.serving.knative.dev unchanged
secret/webhook-certs unchanged
clusterrole.rbac.authorization.k8s.io/knative-serving-istio unchanged
gateway.networking.istio.io/knative-ingress-gateway unchanged
gateway.networking.istio.io/cluster-local-gateway unchanged
gateway.networking.istio.io/knative-local-gateway unchanged
service/knative-local-gateway unchanged
peerauthentication.security.istio.io/webhook unchanged
peerauthentication.security.istio.io/istio-webhook unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.istio.networking.internal.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.istio.networking.internal.knative.dev unchanged
secret/istio-webhook-certs unchanged
configmap/config-istio unchanged
deployment.apps/networking-istio unchanged
deployment.apps/istio-webhook unchanged
service/istio-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
namespace/knative-eventing unchanged
serviceaccount/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-source-observer unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-sources-controller unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-controller-manipulator unchanged
serviceaccount/pingsource-mt-adapter unchanged
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
serviceaccount/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-resolver unchanged
clusterrolebinding.rbac.authorization.k8s.io/eventing-webhook-podspecable-binding unchanged
configmap/config-br-default-channel unchanged
configmap/config-br-defaults unchanged
configmap/default-ch-webhook unchanged
configmap/config-leader-election unchanged
configmap/config-logging unchanged
configmap/config-observability unchanged
configmap/config-tracing unchanged
deployment.apps/eventing-controller unchanged
deployment.apps/pingsource-mt-adapter configured
deployment.apps/eventing-webhook unchanged
service/eventing-webhook unchanged
customresourcedefinition.apiextensions.k8s.io/apiserversources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/brokers.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/channels.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/containersources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/eventtypes.eventing.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/parallels.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/pingsources.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sequences.flows.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/sinkbindings.sources.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/subscriptions.messaging.knative.dev unchanged
customresourcedefinition.apiextensions.k8s.io/triggers.eventing.knative.dev unchanged
clusterrole.rbac.authorization.k8s.io/addressable-resolver configured
clusterrole.rbac.authorization.k8s.io/service-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/serving-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/channel-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/broker-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/messaging-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/flows-addressable-resolver unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-filter unchanged
clusterrole.rbac.authorization.k8s.io/eventing-broker-ingress unchanged
clusterrole.rbac.authorization.k8s.io/eventing-config-reader unchanged
clusterrole.rbac.authorization.k8s.io/channelable-manipulator configured
clusterrole.rbac.authorization.k8s.io/meta-channelable-manipulator unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-messaging-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-flows-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-sources-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-bindings-namespaced-admin unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-edit unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-namespaced-view unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-pingsource-mt-adapter unchanged
clusterrole.rbac.authorization.k8s.io/podspecable-binding configured
clusterrole.rbac.authorization.k8s.io/builtin-podspecable-binding unchanged
clusterrole.rbac.authorization.k8s.io/source-observer configured
clusterrole.rbac.authorization.k8s.io/eventing-sources-source-observer unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-sources-controller unchanged
clusterrole.rbac.authorization.k8s.io/knative-eventing-webhook unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/config.webhook.eventing.knative.dev unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/webhook.eventing.knative.dev unchanged
validatingwebhookconfiguration.admissionregistration.k8s.io/validation.webhook.eventing.knative.dev unchanged
secret/eventing-webhook-certs unchanged
mutatingwebhookconfiguration.admissionregistration.k8s.io/sinkbindings.webhook.sources.knative.dev unchanged
deployment "eventing-controller" successfully rolled out
service/autoscaler annotated
service/autoscaler annotated
service/activator-service annotated
service/activator-service annotated
deployment "eventing-controller" successfully rolled out
deployment "eventing-webhook" successfully rolled out
configmap/config-imc-event-dispatcher created
clusterrole.rbac.authorization.k8s.io/imc-addressable-resolver created
clusterrole.rbac.authorization.k8s.io/imc-channelable-manipulator created
clusterrole.rbac.authorization.k8s.io/imc-controller created
serviceaccount/imc-controller created
clusterrole.rbac.authorization.k8s.io/imc-dispatcher created
service/imc-dispatcher created
serviceaccount/imc-dispatcher created
clusterrolebinding.rbac.authorization.k8s.io/imc-controller created
clusterrolebinding.rbac.authorization.k8s.io/imc-dispatcher created
customresourcedefinition.apiextensions.k8s.io/inmemorychannels.messaging.knative.dev created
deployment.apps/imc-controller created
deployment.apps/imc-dispatcher created
deployment "imc-controller" successfully rolled out
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-channel-broker-controller created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
serviceaccount/mt-broker-filter created
clusterrole.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
serviceaccount/mt-broker-ingress created
clusterrolebinding.rbac.authorization.k8s.io/eventing-mt-channel-broker-controller created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-filter created
clusterrolebinding.rbac.authorization.k8s.io/knative-eventing-mt-broker-ingress created
deployment.apps/mt-broker-filter created
service/broker-filter created
deployment.apps/mt-broker-ingress created
service/broker-ingress created
deployment.apps/mt-broker-controller created
horizontalpodautoscaler.autoscaling/broker-ingress-hpa created
horizontalpodautoscaler.autoscaling/broker-filter-hpa created
deployment "mt-broker-controller" successfully rolled out
deployment "mt-broker-filter" successfully rolled out
+ '[' true = true ']'
+ kubectl apply --filename https://github.com/knative/serving/releases/download/v0.18.0/serving-default-domain.yaml
job.batch/default-domain created
service/default-domain-service created
+ install_argo
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/argo
+ ./argo.sh
namespace/argo created
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/clusterworkflowtemplates.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/cronworkflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workfloweventbindings.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflows.argoproj.io created
customresourcedefinition.apiextensions.k8s.io/workflowtemplates.argoproj.io created
serviceaccount/argo created
serviceaccount/argo-server created
role.rbac.authorization.k8s.io/argo-role created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-admin created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-edit created
clusterrole.rbac.authorization.k8s.io/argo-aggregate-to-view created
clusterrole.rbac.authorization.k8s.io/argo-cluster-role created
clusterrole.rbac.authorization.k8s.io/argo-server-cluster-role created
rolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-binding created
clusterrolebinding.rbac.authorization.k8s.io/argo-server-binding created
configmap/workflow-controller-configmap created
service/argo-server created
service/workflow-controller-metrics created
deployment.apps/argo-server created
deployment.apps/workflow-controller created
configmap/workflow-controller-configmap configured
+ install_minio
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/minio
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./minio.sh
TEMPRESOURCES IS /tmp/tempresources
SD_USER_EMAIL IS admin@seldon-ey.io
namespace/minio-system created
"minio" has been added to your repositories
Release "minio" does not exist. Installing it now.
NAME: minio
LAST DEPLOYED: Wed Oct 20 12:13:45 2021
NAMESPACE: minio-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Minio can be accessed via port 9000 on the following DNS name from within your cluster:
minio.minio-system.svc.cluster.local

To access Minio from localhost, run the below commands:

  1. export POD_NAME=$(kubectl get pods --namespace minio-system -l "release=minio" -o jsonpath="{.items[0].metadata.name}")

  2. kubectl port-forward $POD_NAME 9000 --namespace minio-system

Read more about port forwarding here: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

You can now access Minio server on http://localhost:9000. Follow the below steps to connect to Minio server with mc client:

  1. Download the Minio mc client - https://docs.minio.io/docs/minio-client-quickstart-guide

  2. Get the ACCESS_KEY=$(kubectl get secret minio -o jsonpath="{.data.accesskey}" | base64 --decode) and the SECRET_KEY=$(kubectl get secret minio -o jsonpath="{.data.secretkey}" | base64 --decode)

  3. mc alias set minio-local http://localhost:9000 "$ACCESS_KEY" "$SECRET_KEY" --api s3v4

  4. mc ls minio-local

Alternately, you can use your browser or the Minio SDK to access the server - https://docs.minio.io/categories/17
virtualservice.networking.istio.io/minio created
+ install_EFK_and_logger
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk
+ export TEMPRESOURCES
+ ./install_efk.sh
TEMPRESOURCES IS /tmp/tempresources
Error from server (AlreadyExists): namespaces "seldon-logs" already exists
namespace seldon-logs exists
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/elastic-credentials created
secret/elastic-credentials created
Cloning into 'opendistro-build'...
remote: Enumerating objects: 7421, done.
remote: Counting objects: 100% (531/531), done.
remote: Compressing objects: 100% (246/246), done.
remote: Total 7421 (delta 343), reused 422 (delta 266), pack-reused 6890
Receiving objects: 100% (7421/7421), 1.90 MiB | 805.00 KiB/s, done.
Resolving deltas: 100% (5084/5084), done.
Fetching origin
Note: switching to 'tags/v1.13.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at aabb00f Modify script and workflow for AMI to include ARM64  (#738)
Successfully packaged chart and saved it to: /tmp/tempresources/opendistro-build/helm/opendistro-es/opendistro-es-1.13.2.tgz
Release "elasticsearch" does not exist. Installing it now.
W1020 12:14:37.341245   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:43.646754   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:44.920126   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:57.940282   36513 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:14:59.050377   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:14:59.050983   36513 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
NAME: elasticsearch
LAST DEPLOYED: Wed Oct 20 12:14:34 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
Release "fluentd" does not exist. Installing it now.
WARNING: This chart is deprecated
NAME: fluentd
LAST DEPLOYED: Wed Oct 20 12:15:10 2021
NAMESPACE: seldon-logs
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. To verify that Fluentd has started, run:

  kubectl --namespace=seldon-logs get pods -l "app.kubernetes.io/name=fluentd-elasticsearch,app.kubernetes.io/instance=fluentd"

THIS APPLICATION CAPTURES ALL CONSOLE OUTPUT AND FORWARDS IT TO elasticsearch . Anything that might be identifying,
including things like IP addresses, container images, and object names will NOT be anonymized.
Waiting for deployment "elasticsearch-opendistro-es-kibana" rollout to finish: 0 of 1 updated replicas are available...
deployment "elasticsearch-opendistro-es-kibana" successfully rolled out
+ ./eventing_for_logs_ns.sh
broker.eventing.knative.dev/default created
knative broker created
+ kubectl apply -f /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/efk/kibana-virtualservice.yaml
virtualservice.networking.istio.io/kibana created
+ install_seldon_core
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/seldon-core
+ export TEMPRESOURCES
+ export SELDON_CORE_VERSION
+ export MULTITENANT
+ export EXTERNAL_PROTOCOL
+ ./install_seldon_core.sh
SELDON CORE VERSION v1.9.1
Cloning into 'seldon-core'...
remote: Enumerating objects: 130545, done.
remote: Counting objects: 100% (2898/2898), done.
remote: Compressing objects: 100% (1172/1172), done.
remote: Total 130545 (delta 1846), reused 2511 (delta 1606), pack-reused 127647
Receiving objects: 100% (130545/130545), 212.37 MiB | 824.00 KiB/s, done.
Resolving deltas: 100% (78770/78770), done.
Note: switching to '8ad2ede5ca18e321f8603f1e2a821e767af000de'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

using /tmp/tempresources/seldon-core
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
gateway.networking.istio.io/seldon-gateway configured
Release "seldon-core" does not exist. Installing it now.
W1020 12:21:32.726503   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
W1020 12:21:57.693208   36809 warnings.go:70] admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
NAME: seldon-core
LAST DEPLOYED: Wed Oct 20 12:21:13 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
Waiting for deployment "seldon-controller-manager" rollout to finish: 0 of 1 updated replicas are available...
deployment "seldon-controller-manager" successfully rolled out
+ install_analytics
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/prometheus
+ export TEMPRESOURCES
+ ./seldon-core-analytics.sh
configmap/model-usage-rules created
Error from server (NotFound): deployments.apps "seldon-core-analytics-prometheus-seldon" not found
Release "seldon-core-analytics" does not exist. Installing it now.
W1020 12:28:18.796115   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:20.023979   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:28:49.096327   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:50.323697   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:51.355141   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:52.574403   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:53.599335   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:28:55.648768   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:56.670352   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:57.676505   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:58.922424   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:00.149772   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:01.379295   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:03.834611   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
W1020 12:29:22.466916   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:22.467337   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:25.947779   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.951773   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.988757   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.994807   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.995223   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:26.358782   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358910   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359018   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358798   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359349   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.767071   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:27.176581   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
NAME: seldon-core-analytics
LAST DEPLOYED: Wed Oct 20 12:28:15 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
+ install_kfserving
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/kfserving
+ export TEMPRESOURCES
+ export KFSERVING_TAG
+ ./install_kfserving.sh
TEMPRESOURCES IS /tmp/tempresources
KFSERVING_TAG v0.4.1
Cloning into 'kfserving'...
remote: Enumerating objects: 44567, done.
remote: Counting objects: 100% (1826/1826), done.
remote: Compressing objects: 100% (1192/1192), done.
remote: Total 44567 (delta 839), reused 1249 (delta 566), pack-reused 42741
Receiving objects: 100% (44567/44567), 116.21 MiB | 800.00 KiB/s, done.
Resolving deltas: 100% (17763/17763), done.
Note: switching to 'f253dd529ba25c080ca458d8dc36fd0a19bbd473'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f253dd52 update 0.4.1 yaml (#1176)
using /tmp/tempresources/kfserving
namespace/kfserving-system created
Warning: resource namespaces/kfserving-system is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/kfserving-system configured
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/inferenceservices.serving.kubeflow.org created
Warning: admissionregistration.k8s.io/v1beta1 MutatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 MutatingWebhookConfiguration
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
role.rbac.authorization.k8s.io/leader-election-role created
clusterrole.rbac.authorization.k8s.io/kfserving-manager-role created
clusterrole.rbac.authorization.k8s.io/kfserving-proxy-role created
rolebinding.rbac.authorization.k8s.io/leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-proxy-rolebinding created
configmap/inferenceservice-config created
secret/kfserving-webhook-server-secret created
service/kfserving-controller-manager-metrics-service created
service/kfserving-controller-manager-service created
service/kfserving-webhook-server-service created
statefulset.apps/kfserving-controller-manager created
Warning: admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Certificate" in version "cert-manager.io/v1alpha2"
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Issuer" in version "cert-manager.io/v1alpha2"
configmap/inferenceservice-config patched
service: kfserving-webhook-server-service
namespace: kfserving-system
secret: kfserving-webhook-server-cert
webhookDeploymentName: kfserving-controller-manager-0
webhookConfigName: inferenceservice.serving.kubeflow.org
creating certs in tmpdir /tmp/tmp.VFjc8KH97E 
Generating RSA private key, 2048 bit long modulus (2 primes)
.......................+++++
...........................................................+++++
e is 65537 (0x010001)
Generating RSA private key, 2048 bit long modulus (2 primes)
........................................................................................+++++
......................................................................+++++
e is 65537 (0x010001)
Signature ok
subject=CN = kfserving-webhook-server-service.kfserving-system.svc
Getting CA Private Key
W1020 12:32:50.683819   37974 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
secret/kfserving-webhook-server-cert created
pod "kfserving-controller-manager-0" deleted
webhook kfserving-controller-manager-0 is restarted to utilize the new secret
CA Certificate:
-----BEGIN CERTIFICATE-----
MIIDYTCCAkmgAwIBAgIUIwKbuXlVEBkLnIHYAy0VIOtbhEIwDQYJKoZIhvcNAQEL
BQAwQDE+MDwGA1UEAww1a2ZzZXJ2aW5nLXdlYmhvb2stc2VydmVyLXNlcnZpY2Uu
a2ZzZXJ2aW5nLXN5c3RlbS5zdmMwHhcNMjExMDIwMDcwMjUwWhcNMjIxMDIwMDcw
MjUwWjBAMT4wPAYDVQQDDDVrZnNlcnZpbmctd2ViaG9vay1zZXJ2ZXItc2Vydmlj
ZS5rZnNlcnZpbmctc3lzdGVtLnN2YzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKqYeLIbze8FaJMmaThqsu9gfXsBwXubosNWODeP9KkN1K0MZhPQc2uJ
5fSwW13cxRaXYnOfaT2AmYdXJZKLBKSWCPPli2rIG9sK0uSm6uR6F/wiXRxlhWHI
R2IXzvbChEczanKCj9WGqolBv2pORYToROmtKxrOmgIx80bwWMKRYARskZtXwUe2
q1OYIsjM0iTMxLgTb1sQs1fXXQ2IgGgYXsonK7FRkcfI7mN0BmcOesOnTw1FAcPO
I7D+FKVZfiQxTY8ktx7WxlszKcmh7hd0KOJC2sHfCUJf82O4h8R/ugtSeS/m1K+n
171KW4DpYccvbKDLA8KotO7nTaN5YXcCAwEAAaNTMFEwHQYDVR0OBBYEFNhFaXMQ
qRjegiNmObr9mZHh4QdtMB8GA1UdIwQYMBaAFNhFaXMQqRjegiNmObr9mZHh4Qdt
MA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAA2wU0Ei06Mrd8hW
yscVL1R0odDF5m2pAVhE2Jgig3Di2gLNaEHT0jjOVSWoDRDyxPy8I0a+KirqlWwA
5/2uQiAE60rTLugKO+xdHgkGp3j/QWK6bczlm4S2b5cD0blv+u0TFbnikbKUFRJ1
EpBuLcKWQJUOEvmgtikYeDEsyLrozu8OnxHXiO1bn2ZRPhnDHvbgNb+IeBaeq+a9
NFoN87NOiqXVTxLUt7W4JhazM8ZuOeEfQUzl7k3Wgle9aY37rviD14MMboPigA74
5OB8HTMrpvcCvvqJaszuxirSwHK+y54rKbuNiHQGbnC384viA/JY9qGD4R1kopu0
W+A9NeU=
-----END CERTIFICATE-----
Encoded CA:
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURZVENDQWttZ0F3SUJBZ0lVSXdLYnVYbFZFQmtMbklIWUF5MFZJT3RiaEVJd0RRWUpLb1pJaHZjTkFRRUwKQlFBd1FERStNRHdHQTFVRUF3dzFhMlp6WlhKMmFXNW5MWGRsWW1odmIyc3RjMlZ5ZG1WeUxYTmxjblpwWTJVdQphMlp6WlhKMmFXNW5MWE41YzNSbGJTNXpkbU13SGhjTk1qRXhNREl3TURjd01qVXdXaGNOTWpJeE1ESXdNRGN3Ck1qVXdXakJBTVQ0d1BBWURWUVFERERWclpuTmxjblpwYm1jdGQyVmlhRzl2YXkxelpYSjJaWEl0YzJWeWRtbGoKWlM1clpuTmxjblpwYm1jdGMzbHpkR1Z0TG5OMll6Q0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQwpBUW9DZ2dFQkFLcVllTEliemU4RmFKTW1hVGhxc3U5Z2ZYc0J3WHVib3NOV09EZVA5S2tOMUswTVpoUFFjMnVKCjVmU3dXMTNjeFJhWFluT2ZhVDJBbVlkWEpaS0xCS1NXQ1BQbGkycklHOXNLMHVTbTZ1UjZGL3dpWFJ4bGhXSEkKUjJJWHp2YkNoRWN6YW5LQ2o5V0dxb2xCdjJwT1JZVG9ST210S3hyT21nSXg4MGJ3V01LUllBUnNrWnRYd1VlMgpxMU9ZSXNqTTBpVE14TGdUYjFzUXMxZlhYUTJJZ0dnWVhzb25LN0ZSa2NmSTdtTjBCbWNPZXNPblR3MUZBY1BPCkk3RCtGS1ZaZmlReFRZOGt0eDdXeGxzektjbWg3aGQwS09KQzJzSGZDVUpmODJPNGg4Ui91Z3RTZVMvbTFLK24KMTcxS1c0RHBZY2N2YktETEE4S290TzduVGFONVlYY0NBd0VBQWFOVE1GRXdIUVlEVlIwT0JCWUVGTmhGYVhNUQpxUmplZ2lObU9icjltWkhoNFFkdE1COEdBMVVkSXdRWU1CYUFGTmhGYVhNUXFSamVnaU5tT2JyOW1aSGg0UWR0Ck1BOEdBMVVkRXdFQi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBMndVMEVpMDZNcmQ4aFcKeXNjVkwxUjBvZERGNW0ycEFWaEUySmdpZzNEaTJnTE5hRUhUMGpqT1ZTV29EUkR5eFB5OEkwYStLaXJxbFd3QQo1LzJ1UWlBRTYwclRMdWdLTyt4ZEhna0dwM2ovUVdLNmJjemxtNFMyYjVjRDBibHYrdTBURmJuaWtiS1VGUkoxCkVwQnVMY0tXUUpVT0V2bWd0aWtZZURFc3lMcm96dThPbnhIWGlPMWJuMlpSUGhuREh2YmdOYitJZUJhZXErYTkKTkZvTjg3Tk9pcVhWVHhMVXQ3VzRKaGF6TThadU9lRWZRVXpsN2szV2dsZTlhWTM3cnZpRDE0TU1ib1BpZ0E3NAo1T0I4SFRNcnB2Y0N2dnFKYXN6dXhpclN3SEsreTU0cktidU5pSFFHYm5DMzg0dmlBL0pZOXFHRDRSMWtvcHUwClcrQTlOZVU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K 

patching ca bundle for mutating webhook configuration...
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
patching ca bundle for validating webhook configuration...
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
+ configure_namespaces
+ kubectl create namespace seldon
namespace/seldon created
+ kubectl label ns seldon seldon.restricted=false --overwrite=true
namespace/seldon labeled
+ kubectl label ns seldon serving.kubeflow.org/inferenceservice=enabled --overwrite=true
namespace/seldon labeled
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/configure-batch-on-ns
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./batch-sa-for-ns.sh
TEMPRESOURCES IS /tmp/tempresources
role.rbac.authorization.k8s.io/workflow created
serviceaccount/workflow created
rolebinding.rbac.authorization.k8s.io/workflow created
secret/seldon-job-secret created
Error from server (NotFound): namespaces "kubeflow" not found
secret/seldon-job-secret configured
configured for minio in minio-system
+ install_postgres
+ '[' true = true ']'
+ echo 'Installing postgres...'
Installing postgres...
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/postgres
+ export TEMPRESOURCES
+ export STARTUP_DIR
+ POSTGRES_MANIFEST=minimal-postgres-manifest.yaml
+ ./install_postgres.sh
Installing zalando postgres operator and a db instance if required
Cloning into 'postgres-operator'...
remote: Enumerating objects: 22250, done.
remote: Counting objects: 100% (2142/2142), done.
remote: Compressing objects: 100% (964/964), done.
remote: Total 22250 (delta 1504), reused 1700 (delta 1145), pack-reused 20108
Receiving objects: 100% (22250/22250), 8.71 MiB | 915.00 KiB/s, done.
Resolving deltas: 100% (15803/15803), done.
Note: switching to 'v1.6.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c18241f1 Bump v1.6.2 (#1433)
namespace/postgres created
Release "postgres-operator" does not exist. Installing it now.
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: postgres-operator
LAST DEPLOYED: Wed Oct 20 12:34:07 2021
NAMESPACE: postgres
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that postgres-operator has started, run:

  kubectl --namespace=postgres get pods -l "app.kubernetes.io/name=postgres-operator"
postgresql.acid.zalan.do/seldon-metadata-storage created
The postgres secret has been created by the operator...
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/metadata-postgres created
+ install_keycloak_auth
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/keycloak
+ ./install_keycloak.sh
Error from server (AlreadyExists): namespaces "seldon-system" already exists
secret/realm-secret created
Release "keycloak" does not exist. Installing it now.
NAME: keycloak
LAST DEPLOYED: Wed Oct 20 12:35:16 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
NOTES:
Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  keycloak-http.seldon-system.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

  export POD_NAME=$(kubectl get pods --namespace seldon-system -l app.kubernetes.io/instance=keycloak -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use Keycloak"
  kubectl port-forward --namespace seldon-system $POD_NAME 8080

Login with the following credentials:
Username: "admin@seldon-ey.io"

To retrieve the initial user password run:
kubectl get secret --namespace seldon-system keycloak-http -o jsonpath="{.data.password}" | base64 --decode; echo
virtualservice.networking.istio.io/keycloak created
Waiting for 1 pods to be ready...
statefulset rolling update complete 1 pods at revision keycloak-5d9666fb66...
Creating default keycloak user
 * Default user created
Creating API auth client
 * API client created
 * Keycloak setup completed
[sepoy@xps seldon-deploy-install]$ ./sd-setup/sd-install-default
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/git-creds configured
namespace/argocd configured
Error from server (AlreadyExists): namespaces "seldon-system" already exists
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/request-logger-auth configured
./sd-setup/sd-install-default: line 80: EXTERNAL_HOST: unbound variable
[sepoy@xps seldon-deploy-install]$ ./sd-setup/show-seldon-deploy-url
http://a38fbee579f06403bb22116c69dcb22d-972759690.us-east-2.elb.amazonaws.com/seldon-deploy/
W1020 12:28:57.676505   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:28:58.922424   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:00.149772   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:01.379295   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:03.834611   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
W1020 12:29:22.466916   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:22.467337   37159 warnings.go:70] policy/v1beta1 PodSecurityPolicy is deprecated in v1.21+, unavailable in v1.25+
W1020 12:29:25.947779   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.951773   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.988757   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.994807   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:25.995223   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRole is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRole
W1020 12:29:26.358782   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358910   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359018   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.358798   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.359349   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 ClusterRoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 ClusterRoleBinding
W1020 12:29:26.767071   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 Role is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 Role
W1020 12:29:27.176581   37159 warnings.go:70] rbac.authorization.k8s.io/v1beta1 RoleBinding is deprecated in v1.17+, unavailable in v1.22+; use rbac.authorization.k8s.io/v1 RoleBinding
NAME: seldon-core-analytics
LAST DEPLOYED: Wed Oct 20 12:28:15 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
+ install_kfserving
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/kfserving
+ export TEMPRESOURCES
+ export KFSERVING_TAG
+ ./install_kfserving.sh
TEMPRESOURCES IS /tmp/tempresources
KFSERVING_TAG v0.4.1
Cloning into 'kfserving'...
remote: Enumerating objects: 44567, done.
remote: Counting objects: 100% (1826/1826), done.
remote: Compressing objects: 100% (1192/1192), done.
remote: Total 44567 (delta 839), reused 1249 (delta 566), pack-reused 42741
Receiving objects: 100% (44567/44567), 116.21 MiB | 800.00 KiB/s, done.
Resolving deltas: 100% (17763/17763), done.
Note: switching to 'f253dd529ba25c080ca458d8dc36fd0a19bbd473'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f253dd52 update 0.4.1 yaml (#1176)
using /tmp/tempresources/kfserving
namespace/kfserving-system created
Warning: resource namespaces/kfserving-system is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
namespace/kfserving-system configured
Warning: apiextensions.k8s.io/v1beta1 CustomResourceDefinition is deprecated in v1.16+, unavailable in v1.22+; use apiextensions.k8s.io/v1 CustomResourceDefinition
customresourcedefinition.apiextensions.k8s.io/inferenceservices.serving.kubeflow.org created
Warning: admissionregistration.k8s.io/v1beta1 MutatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 MutatingWebhookConfiguration
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
role.rbac.authorization.k8s.io/leader-election-role created
clusterrole.rbac.authorization.k8s.io/kfserving-manager-role created
clusterrole.rbac.authorization.k8s.io/kfserving-proxy-role created
rolebinding.rbac.authorization.k8s.io/leader-election-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-manager-rolebinding created
clusterrolebinding.rbac.authorization.k8s.io/kfserving-proxy-rolebinding created
configmap/inferenceservice-config created
secret/kfserving-webhook-server-secret created
service/kfserving-controller-manager-metrics-service created
service/kfserving-controller-manager-service created
service/kfserving-webhook-server-service created
statefulset.apps/kfserving-controller-manager created
Warning: admissionregistration.k8s.io/v1beta1 ValidatingWebhookConfiguration is deprecated in v1.16+, unavailable in v1.22+; use admissionregistration.k8s.io/v1 ValidatingWebhookConfiguration
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org created
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Certificate" in version "cert-manager.io/v1alpha2"
unable to recognize "./install/v0.4.1/kfserving.yaml": no matches for kind "Issuer" in version "cert-manager.io/v1alpha2"
configmap/inferenceservice-config patched
service: kfserving-webhook-server-service
namespace: kfserving-system
secret: kfserving-webhook-server-cert
webhookDeploymentName: kfserving-controller-manager-0
webhookConfigName: inferenceservice.serving.kubeflow.org
creating certs in tmpdir /tmp/tmp.VFjc8KH97E 
Generating RSA private key, 2048 bit long modulus (2 primes)
.......................+++++
...........................................................+++++
e is 65537 (0x010001)
Generating RSA private key, 2048 bit long modulus (2 primes)
........................................................................................+++++
......................................................................+++++
e is 65537 (0x010001)
Signature ok
subject=CN = kfserving-webhook-server-service.kfserving-system.svc
Getting CA Private Key
W1020 12:32:50.683819   37974 helpers.go:557] --dry-run is deprecated and can be replaced with --dry-run=client.
secret/kfserving-webhook-server-cert created
pod "kfserving-controller-manager-0" deleted
webhook kfserving-controller-manager-0 is restarted to utilize the new secret
CA Certificate:
-----BEGIN CERTIFICATE-----
MIIDYTCCAkmgAwIBAgIUIwKbuXlVEBkLnIHYAy0VIOtbhEIwDQYJKoZIhvcNAQEL
BQAwQDE+MDwGA1UEAww1a2ZzZXJ2aW5nLXdlYmhvb2stc2VydmVyLXNlcnZpY2Uu
a2ZzZXJ2aW5nLXN5c3RlbS5zdmMwHhcNMjExMDIwMDcwMjUwWhcNMjIxMDIwMDcw
MjUwWjBAMT4wPAYDVQQDDDVrZnNlcnZpbmctd2ViaG9vay1zZXJ2ZXItc2Vydmlj
ZS5rZnNlcnZpbmctc3lzdGVtLnN2YzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCC
AQoCggEBAKqYeLIbze8FaJMmaThqsu9gfXsBwXubosNWODeP9KkN1K0MZhPQc2uJ
5fSwW13cxRaXYnOfaT2AmYdXJZKLBKSWCPPli2rIG9sK0uSm6uR6F/wiXRxlhWHI
R2IXzvbChEczanKCj9WGqolBv2pORYToROmtKxrOmgIx80bwWMKRYARskZtXwUe2
q1OYIsjM0iTMxLgTb1sQs1fXXQ2IgGgYXsonK7FRkcfI7mN0BmcOesOnTw1FAcPO
I7D+FKVZfiQxTY8ktx7WxlszKcmh7hd0KOJC2sHfCUJf82O4h8R/ugtSeS/m1K+n
171KW4DpYccvbKDLA8KotO7nTaN5YXcCAwEAAaNTMFEwHQYDVR0OBBYEFNhFaXMQ
qRjegiNmObr9mZHh4QdtMB8GA1UdIwQYMBaAFNhFaXMQqRjegiNmObr9mZHh4Qdt
MA8GA1UdEwEB/wQFMAMBAf8wDQYJKoZIhvcNAQELBQADggEBAA2wU0Ei06Mrd8hW
yscVL1R0odDF5m2pAVhE2Jgig3Di2gLNaEHT0jjOVSWoDRDyxPy8I0a+KirqlWwA
5/2uQiAE60rTLugKO+xdHgkGp3j/QWK6bczlm4S2b5cD0blv+u0TFbnikbKUFRJ1
EpBuLcKWQJUOEvmgtikYeDEsyLrozu8OnxHXiO1bn2ZRPhnDHvbgNb+IeBaeq+a9
NFoN87NOiqXVTxLUt7W4JhazM8ZuOeEfQUzl7k3Wgle9aY37rviD14MMboPigA74
5OB8HTMrpvcCvvqJaszuxirSwHK+y54rKbuNiHQGbnC384viA/JY9qGD4R1kopu0
W+A9NeU=
-----END CERTIFICATE-----
Encoded CA:
LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURZVENDQWttZ0F3SUJBZ0lVSXdLYnVYbFZFQmtMbklIWUF5MFZJT3RiaEVJd0RRWUpLb1pJaHZjTkFRRUwKQlFBd1FERStNRHdHQTFVRUF3dzFhMlp6WlhKMmFXNW5MWGRsWW1odmIyc3RjMlZ5ZG1WeUxYTmxjblpwWTJVdQphMlp6WlhKMmFXNW5MWE41YzNSbGJTNXpkbU13SGhjTk1qRXhNREl3TURjd01qVXdXaGNOTWpJeE1ESXdNRGN3Ck1qVXdXakJBTVQ0d1BBWURWUVFERERWclpuTmxjblpwYm1jdGQyVmlhRzl2YXkxelpYSjJaWEl0YzJWeWRtbGoKWlM1clpuTmxjblpwYm1jdGMzbHpkR1Z0TG5OMll6Q0NBU0l3RFFZSktvWklodmNOQVFFQkJRQURnZ0VQQURDQwpBUW9DZ2dFQkFLcVllTEliemU4RmFKTW1hVGhxc3U5Z2ZYc0J3WHVib3NOV09EZVA5S2tOMUswTVpoUFFjMnVKCjVmU3dXMTNjeFJhWFluT2ZhVDJBbVlkWEpaS0xCS1NXQ1BQbGkycklHOXNLMHVTbTZ1UjZGL3dpWFJ4bGhXSEkKUjJJWHp2YkNoRWN6YW5LQ2o5V0dxb2xCdjJwT1JZVG9ST210S3hyT21nSXg4MGJ3V01LUllBUnNrWnRYd1VlMgpxMU9ZSXNqTTBpVE14TGdUYjFzUXMxZlhYUTJJZ0dnWVhzb25LN0ZSa2NmSTdtTjBCbWNPZXNPblR3MUZBY1BPCkk3RCtGS1ZaZmlReFRZOGt0eDdXeGxzektjbWg3aGQwS09KQzJzSGZDVUpmODJPNGg4Ui91Z3RTZVMvbTFLK24KMTcxS1c0RHBZY2N2YktETEE4S290TzduVGFONVlYY0NBd0VBQWFOVE1GRXdIUVlEVlIwT0JCWUVGTmhGYVhNUQpxUmplZ2lObU9icjltWkhoNFFkdE1COEdBMVVkSXdRWU1CYUFGTmhGYVhNUXFSamVnaU5tT2JyOW1aSGg0UWR0Ck1BOEdBMVVkRXdFQi93UUZNQU1CQWY4d0RRWUpLb1pJaHZjTkFRRUxCUUFEZ2dFQkFBMndVMEVpMDZNcmQ4aFcKeXNjVkwxUjBvZERGNW0ycEFWaEUySmdpZzNEaTJnTE5hRUhUMGpqT1ZTV29EUkR5eFB5OEkwYStLaXJxbFd3QQo1LzJ1UWlBRTYwclRMdWdLTyt4ZEhna0dwM2ovUVdLNmJjemxtNFMyYjVjRDBibHYrdTBURmJuaWtiS1VGUkoxCkVwQnVMY0tXUUpVT0V2bWd0aWtZZURFc3lMcm96dThPbnhIWGlPMWJuMlpSUGhuREh2YmdOYitJZUJhZXErYTkKTkZvTjg3Tk9pcVhWVHhMVXQ3VzRKaGF6TThadU9lRWZRVXpsN2szV2dsZTlhWTM3cnZpRDE0TU1ib1BpZ0E3NAo1T0I4SFRNcnB2Y0N2dnFKYXN6dXhpclN3SEsreTU0cktidU5pSFFHYm5DMzg0dmlBL0pZOXFHRDRSMWtvcHUwClcrQTlOZVU9Ci0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K 

patching ca bundle for mutating webhook configuration...
mutatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
patching ca bundle for validating webhook configuration...
validatingwebhookconfiguration.admissionregistration.k8s.io/inferenceservice.serving.kubeflow.org patched
+ configure_namespaces
+ kubectl create namespace seldon
namespace/seldon created
+ kubectl label ns seldon seldon.restricted=false --overwrite=true
namespace/seldon labeled
+ kubectl label ns seldon serving.kubeflow.org/inferenceservice=enabled --overwrite=true
namespace/seldon labeled
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/configure-batch-on-ns
+ export TEMPRESOURCES
+ export SD_USER_EMAIL
+ export SD_PASSWORD
+ export STARTUP_DIR
+ ./batch-sa-for-ns.sh
TEMPRESOURCES IS /tmp/tempresources
role.rbac.authorization.k8s.io/workflow created
serviceaccount/workflow created
rolebinding.rbac.authorization.k8s.io/workflow created
secret/seldon-job-secret created
Error from server (NotFound): namespaces "kubeflow" not found
secret/seldon-job-secret configured
configured for minio in minio-system
+ install_postgres
+ '[' true = true ']'
+ echo 'Installing postgres...'
Installing postgres...
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/postgres
+ export TEMPRESOURCES
+ export STARTUP_DIR
+ POSTGRES_MANIFEST=minimal-postgres-manifest.yaml
+ ./install_postgres.sh
Installing zalando postgres operator and a db instance if required
Cloning into 'postgres-operator'...
remote: Enumerating objects: 22250, done.
remote: Counting objects: 100% (2142/2142), done.
remote: Compressing objects: 100% (964/964), done.
remote: Total 22250 (delta 1504), reused 1700 (delta 1145), pack-reused 20108
Receiving objects: 100% (22250/22250), 8.71 MiB | 915.00 KiB/s, done.
Resolving deltas: 100% (15803/15803), done.
Note: switching to 'v1.6.2'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at c18241f1 Bump v1.6.2 (#1433)
namespace/postgres created
Release "postgres-operator" does not exist. Installing it now.
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
manifest_sorter.go:192: info: skipping unknown hook: "crd-install"
NAME: postgres-operator
LAST DEPLOYED: Wed Oct 20 12:34:07 2021
NAMESPACE: postgres
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
To verify that postgres-operator has started, run:

  kubectl --namespace=postgres get pods -l "app.kubernetes.io/name=postgres-operator"
postgresql.acid.zalan.do/seldon-metadata-storage created
The postgres secret has been created by the operator...
Error from server (AlreadyExists): namespaces "seldon-system" already exists
namespace seldon-system exists
secret/metadata-postgres created
+ install_keycloak_auth
+ cd /home/sepoy/Desktop/trail/seldon-deploy-install/prerequisites-setup/keycloak
+ ./install_keycloak.sh
Error from server (AlreadyExists): namespaces "seldon-system" already exists
secret/realm-secret created
Release "keycloak" does not exist. Installing it now.
NAME: keycloak
LAST DEPLOYED: Wed Oct 20 12:35:16 2021
NAMESPACE: seldon-system
STATUS: deployed
REVISION: 1
NOTES:
Keycloak can be accessed:

* Within your cluster, at the following DNS name at port 80:

  keycloak-http.seldon-system.svc.cluster.local

* From outside the cluster, run these commands in the same shell:

  export POD_NAME=$(kubectl get pods --namespace seldon-system -l app.kubernetes.io/instance=keycloak -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use Keycloak"
  kubectl port-forward --namespace seldon-system $POD_NAME 8080

Login with the following credentials:
Username: "admin@seldon-ey.io"

To retrieve the initial user password run:
kubectl get secret --namespace seldon-system keycloak-http -o jsonpath="{.data.password}" | base64 --decode; echo
virtualservice.networking.istio.io/keycloak created
Waiting for 1 pods to be ready...
statefulset rolling update complete 1 pods at revision keycloak-5d9666fb66...
Creating default keycloak user
 * Default user created
Creating API auth client
 * API client created
 * Keycloak setup completed
[sepoy@xps seldon-deploy-install]$ ./sd-setup/sd-install-default
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/git-creds configured
namespace/argocd configured
Error from server (AlreadyExists): namespaces "seldon-system" already exists
running check-config ...
found config file
/home/sepoy/.config/seldon/seldon-deploy/sdconfig.txt
secret/request-logger-auth configured
./sd-setup/sd-install-default: line 80: EXTERNAL_HOST: unbound variable
[sepoy@xps seldon-deploy-install]$ ./sd-setup/show-seldon-deploy-url
http://a38fbee579f06403bb22116c69dcb22d-972759690.us-east-2.elb.amazonaws.com/seldon-deploy/

[sepoy@xps seldon-deploy-install]$ ./sd-setup/show-seldon-deploy-url
http://a38fbee579f06403bb22116c69dcb22d-972759690.us-east-2.elb.amazonaws.com/seldon-deploy/

