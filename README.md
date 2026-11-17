# lab

* runs on k3s with metallb ~~minikube w colima~~
  * `curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--disable servicelb" sh -` <- has traefik by default
* main apps:
  * gitlab, running w/ garage storage
  * dotadle (backend only rn), ~~available @ `dotadle.satyrikon`~~
  * ~~emby @ `emby.satyrikon`~~
* [under construction] other components:
  * kube-prometheus-stack, grafana @ `grafana.satyrikon`
  * local docker registry @ `registry.satyrikon`
  * cert-manager
* to add:
  * [klandestin](https://github.com/euocheisthai/klandestin) currently running the caveman way (and it's likely to stay this way)
  * proper dns management probably using [external-dns](https://github.com/kubernetes-sigs/external-dns)
  * [loxosceles](https://github.com/euocheisthai/loxosceles) once it's finished
