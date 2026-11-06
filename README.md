# lab

* runs on ~~k3s~~ minikube
    * on mac socket_vmnet is required https://minikube.sigs.k8s.io/docs/drivers/qemu/
    * `minikube start --driver docker`
    * `minikube addons enable metallb && minikube addons configure metallb`
    * `minikube addons open traefik && minikube service traefik -n kube-system`
* main apps:
    * dotadle (backend only rn), available @ `dotadle.satyrikon`
    * emby @ `emby.satyrikon`
* other components:
    * kube-prometheus-stack, grafana @ `grafana.satyrikon`
    * local docker registry @ `registry.satyrikon`
    * cert-manager
    * traefik
* to add:
    * gitea
    * [klandestin](https://github.com/euocheisthai/klandestin) currently running the caveman way
    * the way dns is managed
    * [loxosceles](https://github.com/euocheisthai/loxosceles) once it's finished
