# lab

* runs on ~~k3s~~ minikube
    * `minikube start --driver docker`
    * `minikube addons enable metallb && minikube addons configure metallb`
    * `minikube addons open traefik && minikube service traefik -n kube-system`
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
