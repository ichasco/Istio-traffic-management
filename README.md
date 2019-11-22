# Istio Traffic Management

## Install Istio

### Install Istioctl

```
curl -L https://istio.io/downloadIstio | ISTIO_VERSION=1.4.0 sh -
cd istio-1.4.0
export PATH=$PWD/bin:$PATH
```

### Deploy Istio

```
istioctl manifest apply  \
    --set values.gateways.istio-egressgateway.enabled=true \
    --set values.tracing.enabled=true \
    --set values.grafana.enabled=true \
    --set values.kiali.enabled=true \
    --set "values.kiali.dashboard.jaegerURL=http://jaeger-query:16686" \
    --set "values.kiali.dashboard.grafanaURL=http://grafana:3000"
```

## Load test

`siege -c 5 -r 1000 http://traffic-split.35.240.106.245.nip.io/`