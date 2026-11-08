# lab

* runs on ~~k3s~~ minikube w colima
    * `colima start --cpu 8 --memory 20`
    * `minikube start  --driver docker -p minikube --cpus=6 --memory=16384 --addons metallb,traefik` ([1])
    * `minikube addons configure metallb`
    * `minikube service traefik -n kube-system`
* main apps:
    * dotadle (backend only rn), ~~available @ `dotadle.satyrikon`~~
    * ~~emby @ `emby.satyrikon`~~
* other components:
    * kube-prometheus-stack, grafana @ `grafana.satyrikon`
    * local docker registry @ `registry.satyrikon`
    * cert-manager
    * traefik
* to add:
    * [klandestin](https://github.com/euocheisthai/klandestin) currently running the caveman way
    * proper dns management probably using [external-dns](https://github.com/kubernetes-sigs/external-dns)
    * [loxosceles](https://github.com/euocheisthai/loxosceles) once it's finished


---
(1) traefik loadbalancer pool needs to be allocated on the same subnet as the docker subnet (e.g. `192.168.49.200-192.168.49.250` if minikube runs on `192.168.49.0/24`), so check that all of that matches up:
```
minikube ip
docker network inspect minikube [--format '{{json .IPAM.Config}}]
k -n metallb-system get configmap config -o yaml
```

At the very least connecting thru coliima should work: `colima ssh -- curl -v --noproxy '*' --connect-timeout 5 --max-time 10 -H 'Host: admin.storage-nas.satyrikon' http://192.168.49.200/health`. On mac i need to setup port forwarding too, e.g. 127.0.0.1:18080 --> 192.168.49.200:80:  `ssh -F /etc/ssh/colima_ssh_config -S none -o ExitOnForwardFailure=yes -N -L 127.0.0.1:18080:192.168.49.200:80 colima`