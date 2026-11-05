https://docs.gitlab.com/runner/install/kubernetes/

https://docs.gitlab.com/charts/installation/tools/

TODO
set up redis + psql
set up gitlab
set up gitlab runners
???
set up ci?

## components

### postgres

```
k create secret generic postgres-secret --from-literal=password=<pass>

k create configmap postgres-config --from-file=postgresql.conf --from-file=pg_hba.conf
```