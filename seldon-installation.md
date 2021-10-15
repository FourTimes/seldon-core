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
 kubectl get all -n istio-operator

```

Uninstall the control-plane

```bash
istioctl operator remove
```


Istio control-plane installation

```bash

kubectl create ns istio-system

```

```yml
# vim istio-control-plane.yml
apiVersion: install.istio.io/v1alpha1
kind: IstioOperator
metadata:
  namespace: istio-system
  name: istio-control-plane
spec:
  profile: demo
  
```

```bash

vim istio-control-plane.yml
kubectl apply -f istio-control-plane.yml

```

uninstall istio-control-plane (If Required)

```bash

kubectl delete -f istio-control-plane.yml
or
kubectl delete iop -n istio-system istio-control-plane

```


