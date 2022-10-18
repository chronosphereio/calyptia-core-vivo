# Fluent-bit data visualizer

## Development

```bash
docker compose up
```

## Production

To deploy in Kubernetes a YAML file is provided locally: [`kubectl apply -f ./vivo-k8s.yaml`](./vivo-k8s.yaml).

This provides a ClusterIP service so can be accessed anywhere in the cluster but external access requires an ingress and/or NodePort/LoadBalancer service.

An example using KIND with Ingress from <http://localhost> is shown below:

```shell
kind create cluster --config=./kind/config.yaml
kubectl apply -f ./vivo-k8s.yaml
./kind/setup-ingress.sh
```

This uses the set up as described in the KIND documentation just to forward all traffic to the HTTP service for Vivo: <https://kind.sigs.k8s.io/docs/user/ingress/>.

### Run latest build

```bash
docker run -ti --rm --name=vivo -p5489:5489 -p24224:24224 ghcr.io/calyptia/vivo
```

### Build locally

```bash
docker build -t vivo --target=prod .
docker run -ti --rm --name=vivo -p5489:5489 -p24224:24224 vivo
```
