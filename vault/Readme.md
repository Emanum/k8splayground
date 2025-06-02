# Tutorial: Deploying HashiCorp Vault on Kubernetes using Helm

bash:

```
helm repo add hashicorp https://helm.releases.hashicorp.com
helm install -f rancher-desktop vault hashicorp/vault
```

or upgrade

```bash
helm upgrade -f rancher-desktop vault hashicorp/vault
```

## FAQ Accessing Vault

Should be accessible at https://vault.127.0.0.1.sslip.io

Sometimes the DNS of the router is blocking sslip for local addresses. One way to resolve this is to change the DNS
server to 1.1.1.1 or some other public DNS server in the network settings of your computer.
Otherwise, you can try to change the /etc/hosts file to add the following entry:

```plaintext
vault.127.0.0.1.sslip.io 127.0.0.1
```