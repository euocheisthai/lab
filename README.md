# lab

* runs on k3s with metallb ~~minikube w colima~~
  * `curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--disable servicelb" sh -` <- has traefik by default
* [under construction] main components and apps:
  * [up] gitlab, running w/ garage storage (eventually will be employed to test [my suckess setup](https://github.com/euocheisthai/archfiles) w/ xephyr in there)
  * [up] kube-prometheus-stack, grafana @ `grafana.satyrikon`
  * [up] [klandestin](https://github.com/euocheisthai/klandestin) currently running the caveman way (and it's likely to stay this way)
  * [wip] dotadle @ `dotadle.satyrikon`
  * [wip] proper dns management probably using [external-dns](https://github.com/kubernetes-sigs/external-dns)
  * [wip] [loxosceles](https://github.com/euocheisthai/loxosceles) once it's finished
  * [down] emby @ `emby.satyrikon`
  * [down] local docker registry @ `registry.satyrikon`
