# Ingress deployment example

## Deploy cluster
```
sudo kubeadm init --pod-network-cidr 10.244.0.0/16 --kubernetes-version 1.30.0
```
## Deploy Flannel
```
kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
```
## Deploy MetalLB
```
kubectl get configmap kube-proxy -n kube-system -o yaml | sed -e "s/strictARP: false/strictARP: true/" | kubectl apply -f - -n kube-system
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.7/config/manifests/metallb-native.yaml
kubectl apply -f metallb-pool.yaml
```
## Deploy Kong
```
kubectl apply -f https://bit.ly/k4k8s
```
## Deploy examples
```
kubectl apply -f 2048-ingress.yaml
kubectl apply -f echoserver-ingress.yaml
```
