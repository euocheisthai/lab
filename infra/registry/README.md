
- `docker run --rm --entrypoint htpasswd registry:2.7.0 -Bbn <user> <password> > auth_htpasswd`
- `k create secret generic registry-secret --from-file=auth_htpasswd`
- `k apply -f /Users/melvins/stuffs/lab/infra/registry/pvc.registry.yaml`
- create the cert

```
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=registry.satyrikon"

k create secret tls docker-registry-tls --key tls.key --cert tls.crt --namespace default

```
- fill out values.yaml
- `helm install -f values.yaml docker-registry --namespace default twuni/docker-registry`