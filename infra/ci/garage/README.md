for traefik, [install](https://doc.traefik.io/traefik/reference/install-configuration/providers/kubernetes/kubernetes-crd/) crds and rbac first:

```
# Install Traefik Resource Definitions:
k apply -f https://raw.githubusercontent.com/traefik/traefik/v3.7/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml

# Install RBAC for Traefik:
k apply -f https://raw.githubusercontent.com/traefik/traefik/v3.7/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
```