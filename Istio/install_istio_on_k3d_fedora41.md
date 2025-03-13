# Install Istio on K3d on Fedora 41

[Istio][00] is a [service mesh][01] that is broadly used in kubernetes.

The [course on udemy][02] that I was doing to learn about it suggested to use
[minikube][04] as a platform to experiment locally, but I wanted to try out and
learn about [k3d][03] instead.

There is document about k3d from Istio team, but that led me to a very barebones
installation. Here are the steps that I followed to get a more complete install
on Fedora 41 and deploy the sample course application on the cluster.

Pre-requisite: [helm][05] needs to be already installed on the host.

## Ensure that kernel modules needed by Istio are loaded

This solution was copied from [Github][09], here is the list of needed modules:

```
br_netfilter
nf_nat
xt_REDIRECT
xt_owner
iptable_nat
iptable_mangle
iptable_filter
```

Since `k3d` runs on docker, the cluster nodes are effectively using the same kernel as the
host. If this was a production-like cluster were worker nodes are separate hosts, modules
need to be loaded on each worker.

I added the modules to `/etc/modules-load.d/istio-iptables.conf` on my host,
and also ran `sudo modprobe <module>` to load the ones that were not loaded the first
time that I played with this.

## Create a cluster without traefik (adjust servers/agents to your needs!)

```console
> k3d cluster create \
    --api-port 6550 \
    -p '9080:80@loadbalancer' \
    -p '9443:443@loadbalancer' \
    --servers 3 \
    --agents 2 \
    --k3s-arg '--disable=traefik@server:*'
```

## Setup Istio

These commands install the core Istio into the `istio-system` namespace.

```console
> kubectl create namespace istio-system
> helm install istio-base istio/base -n istio-system --wait
> helm install istiod istio/istiod -n istio-system --wait
```

## Install ingress gateway

Not 100% sure if this is needed, but I went ahead anyway.

```console
> helm install istio-ingressgateway istio/gateway -n istio-system --wait
```

## Install addons

[Prometheus][06] is needed for telemetry. [Kiali][07] and [Grafana][08] make use of these metrics
to visualize the information. Customize `ISTIO_VERSION` to your needs.

```console
> ISTIO_VERSION="1.25"
> kubectl apply -f "https://raw.githubusercontent.com/istio/istio/release-${ISTIO_VERSION}/samples/addons/prometheus.yaml"
> kubectl apply -f "https://raw.githubusercontent.com/istio/istio/release-${ISTIO_VERSION}/samples/addons/kiali.yaml"
> kubectl apply -f "https://raw.githubusercontent.com/istio/istio/release-${ISTIO_VERSION}/samples/addons/grafana.yaml"
```

## Enable proxy injection on the namespace where resources are to be deployed

This ensures that envoy proxy container is injected into each pod. You can verify it
by listing pods afterwards, and seeing that all them have an extra container.

```console
> kubectl label namespace default istio-injection=enabled
```

## Deploy the application

The sample application from the course can finally be deployed (note that by default
it comes with some network failures to prove how Istio can help troubleshooting!).

See that all pods have `2/2` containers ready: one with the business logic, and the envoy proxy that
was injected by Istio.

```console
> git clone https://github.com/DickChesterwood/istio-fleetman.git
> kubectl apply -f istio-fleetman/_course_files/x86_amd64/warmup-exercise/4-application-full-stack.yaml
> kubectl get pods
NAME                                  READY   STATUS    RESTARTS      AGE
api-gateway-598764d687-cpg4p          2/2     Running   4 (35m ago)   8h
photo-service-64fcb5ff6-5g54b         2/2     Running   4 (35m ago)   8h
position-simulator-59fb4b9bcc-5c4xh   2/2     Running   0             35m
position-tracker-554d9fbb99-7vvcg     2/2     Running   0             35m
staff-service-5796b965f4-gpkjn        2/2     Running   4 (36m ago)   8h
vehicle-telemetry-699746776c-cnq7z    2/2     Running   0             35m
webapp-6b8c8c65c6-lgc7h               2/2     Running   0             35m
```

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://istio.io/
[01]: https://en.wikipedia.org/wiki/Service_mesh
[02]: https://www.udemy.com/course/istio-hands-on-for-kubernetes/
[03]: https://k3d.io/
[04]: https://minikube.sigs.k8s.io/docs/
[05]: https://helm.sh/
[06]: https://istio.io/latest/docs/ops/integrations/prometheus/
[07]: https://istio.io/latest/docs/ops/integrations/kiali/
[08]: https://istio.io/latest/docs/ops/integrations/grafana/
[09]: https://github.com/istio/istio/issues/44118#issuecomment-1486226384
