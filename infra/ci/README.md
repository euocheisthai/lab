## prep

application order: gitlab-base -> postgres (don't forget the secrets) -> redis -> garage (generate keys w `openssl rand -hex 32/16`)

## gitlab deployment

### postgres

to be moved to some ci migration/k8s job:
```sh
k -n gitlab exec postgres-gitlab-0 -- createdb -U admuser gitlabhq_production
k -n gitlab exec postgres-gitlab-0 -- psql -U admuser -d gitlabhq_production -v ON_ERROR_STOP=1 -c 'CREATE EXTENSION IF NOT EXISTS amcheck; CREATE EXTENSION IF NOT EXISTS pg_trgm; CREATE EXTENSION IF NOT EXISTS btree_gist;'
```

### garage

saved this to `~/lab/infra/ci/garage/garage_connection`, same creds as the garage replicaset ones:

```yaml
provider: AWS
region: us-east-1
endpoint: http://garage-s3-service.gitlab.svc.cluster.local:3900
path_style: true
aws_access_key_id: "<gitlab garage key id>"
aws_secret_access_key: "<gitlab garage secret keu>"
```

then create the secret w/ same creds and run the job:
```sh
k -n gitlab create secret generic gitlab-rails-storage --from-file=connection=~/lab/infra/ci/garage/garage_connection --from-literal=access-key-id='<gitlab garage key id>' --dry-run=client -o yaml | k apply --server-side -f -
k apply -f ~/lab/infra/ci/garage/08-job.gitlab-buckets.yaml
k -n gitlab wait --for=condition=complete job/garage-gitlab-buckets --timeout=5m
k -n gitlab logs job/garage-gitlab-buckets
```

### rendering gitlab helm chart

```sh
helm repo add gitlab https://charts.gitlab.io/
helm repo update gitlab
helm search repo gitlab/gitlab --versions

helm template gitlab gitlab/gitlab -n gitlab --version "10.5.7" -f ~/lab/infra/ci/gitlab/lab.values.yaml > /tmp/gitlab-rendered.yaml 
# ^ check for bullshit

helm upgrade --install gitlab gitlab/gitlab -n gitlab --version "10.5.7" -f ~/lab/infra/ci/gitlab/lab.values.yaml --wait
# ^ this will take a while
```

### checking whether it works

at this point /etc/hosts should contain a record of the cluster external ip mapping to gitlab.satyrikon. In case it doesn't (or i'm on mac again)...

`curl --resolve gitlab.satyrikon:80:10.43.0.100 http://gitlab.satyrikon/-/readiness`

### adding runners

saved the auth token to an ignored file `~/lab/infra/ci/gitlab-runners/auth-token`.

```sh
k -n gitlab-runners create secret generic gitlab-runner-auth --from-file=runner-token=~/lab/infra/ci/gitlab-runners/auth-token --from-literal=runner-registration-token=''

helm search repo gitlab/gitlab-runner --versions

helm upgrade --install gitlab-runner gitlab/gitlab-runner -n gitlab-runners --version "0.94.3" -f ~lab/infra/ci/gitlab/runner.lab.values.yaml --wait
```