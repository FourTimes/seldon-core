Installtion seldon-core


Pre-requirements

    1. Istio
    2. seldon core
    3. seldon deploy

Istio installtion process

```bash

export ISTIO_VERSION=1.7.3
curl -L https://istio.io/downloadIstio | ISTIO_VERSION=${ISTIO_VERSION} sh -
cd istio-${ISTIO_VERSION}
export PATH="$PATH:$PWD/bin"

```

Istio Opearator installation process

```bash

 istioctl operator init

```


Istio control-plane installation

```bash

kubecl create ns istio-system

```

```yml

apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  namespace: istio-system
  name: istiocontrolplane
spec:
  profile: demo
  
```
