# K3D

``` bash
k3d cluster create -p "80:80@loadbalancer" -p "443:443@loadbalancer" --servers 3
```

Switching context to the new cluster:

``` bash
k3d cluster list
k3d kubeconfig get k3s-default >> ~/.kube/config
kubectl config use-context k3d-k3s-default
```

## Install Cert Manager

``` bash
helm repo add jetstack https://charts.jetstack.io --force-update
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.17.2 \
  --set crds.enabled=true
```


## Install Rancher UI 

``` bash
helm repo add rancher-latest https://releases.rancher.com/server-charts/latest
helm install rancher rancher-latest/rancher \
  --namespace cattle-system \
  --create-namespace \
  --set hostname=k8s.127-0-0-1.sslip.io \
  --set replicas=1 \
  --set bootstrapPassword=topSecret
```

Then go to https://k8s.127-0-0-1.sslip.io and login with the password `topSecret`. If 


## FAQ SSLIP.IO

Sometimes the DNS of the router is blocking sslip for local addresses. One way to resolve this is to change the DNS
server to 1.1.1.1 or some other public DNS server in the network settings of your computer.
Otherwise, you can try to change the /etc/hosts file to add the following entry:

```plaintext
k8s.127-0-0-1.sslip.io 127.0.0.1
```
