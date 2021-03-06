```yml
# helm get values seldon-core
ambassador:
  enabled: true
  singleNamespace: false
certManager:
  enabled: false
controllerId: ""
crd:
  create: true
  forceV1: false
  forceV1beta1: false
credentials:
  gcs:
    gcsCredentialFileName: gcloud-application-credentials.json
  s3:
    s3AccessKeyIDName: awsAccessKeyID
    s3SecretAccessKeyName: awsSecretAccessKey
defaultUserID: "8888"
engine:
  grpc:
    port: 5001
  image:
    pullPolicy: IfNotPresent
    registry: docker.io
    repository: seldonio/engine
    tag: 1.9.1
  logMessagesExternally: false
  port: 8000
  prometheus:
    path: /prometheus
  resources:
    cpuLimit: 500m
    cpuRequest: 500m
    memoryLimit: 512Mi
    memoryRequest: 512Mi
  serviceAccount:
    name: default
  user: 8888
executor:
  image:
    pullPolicy: IfNotPresent
    registry: docker.io
    repository: seldonio/seldon-core-executor
    tag: 1.9.1
  metricsPortName: metrics
  port: 8000
  prometheus:
    path: /prometheus
  requestLogger:
    defaultEndpoint: http://default-broker
  resources:
    cpuLimit: 500m
    cpuRequest: 500m
    memoryLimit: 512Mi
    memoryRequest: 512Mi
  serviceAccount:
    name: default
  user: 8888
explainer:
  image: seldonio/alibiexplainer:1.9.1
image:
  pullPolicy: IfNotPresent
  registry: docker.io
  repository: seldonio/seldon-core-operator
  tag: 1.9.1
istio:
  enabled: false
  gateway: istio-system/seldon-gateway
  tlsMode: ""
keda:
  enabled: false
kubeflow: false
manager:
  cpuLimit: 500m
  cpuRequest: 100m
  logLevel: INFO
  memoryLimit: 300Mi
  memoryRequest: 200Mi
managerCreateResources: false
managerUserID: 8888
namespaceOverride: ""
predictiveUnit:
  defaultEnvSecretRefName: ""
  grpcPort: 9500
  httpPort: 9000
  metricsPortName: metrics
predictor_servers:
  MLFLOW_SERVER:
    protocols:
      seldon:
        defaultImageVersion: 1.9.1
        image: seldonio/mlflowserver
  SKLEARN_SERVER:
    protocols:
      kfserving:
        defaultImageVersion: 0.3.2
        image: seldonio/mlserver
      seldon:
        defaultImageVersion: 1.9.1
        image: seldonio/sklearnserver
  TEMPO_SERVER:
    protocols:
      kfserving:
        defaultImageVersion: 0.3.2
        image: seldonio/mlserver
  TENSORFLOW_SERVER:
    protocols:
      seldon:
        defaultImageVersion: 1.9.1
        image: seldonio/tfserving-proxy
      tensorflow:
        defaultImageVersion: 2.1.0
        image: tensorflow/serving
  TRITON_SERVER:
    protocols:
      kfserving:
        defaultImageVersion: 20.08-py3
        image: nvcr.io/nvidia/tritonserver
  XGBOOST_SERVER:
    protocols:
      kfserving:
        defaultImageVersion: 0.3.2
        image: seldonio/mlserver
      seldon:
        defaultImageVersion: 1.9.1
        image: seldonio/xgboostserver
rbac:
  configmap:
    create: true
  create: true
serviceAccount:
  create: true
  name: seldon-manager
singleNamespace: false
storageInitializer:
  cpuLimit: "1"
  cpuRequest: 100m
  image: seldonio/rclone-storage-initializer:1.9.1
  memoryLimit: 1Gi
  memoryRequest: 100Mi
usageMetrics:
  enabled: false
webhook:
  port: 4443



```
