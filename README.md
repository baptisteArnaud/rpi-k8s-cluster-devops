# Raspberry Pi DevOps K8S
My own devops config using Raspberry Pi based k8s cluster including Owncloud, Website hosting, DLNA server, Torrents seeder and possibly anything you can imagine.
## Prerequisite
You need at least a Raspberry Pi with Kubernetes installed. I personnally followed [this tutorial](https://kubecloud.io/setting-up-a-kubernetes-1-11-raspberry-pi-cluster-using-kubeadm-952bbda329c8).

Create TLS certificate that we'll use for UI:
```
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout ./tls.key -out ./tls.crt -subj "/CN=*.example.com"
```
Replace `example.com` by anything you want

# Get started
## Traefik Controller
First of all, you need to setup an Ingress Controller in order to handle applications load balancing. More info [here](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/).
I chose to implement Traefik.

Paste these values in secret that is described in `traefik-controller/tls_secret.yaml`:
```
cat tls.crt | base64 -w0
```
```
cat tls.key | base64 -w0
```

Install the traefik controller:
```
$ kubectl apply -f ./traefik-controller/
```
---

From now on, every services deployed can follow these config patterns : 3 files -> deployment.yaml (pod specs), service.yaml (exposed service), ingress.yaml (routing and naming).

We'll use Helm in order to variabalize our config and handle services as packages. See [Helm Quickstart Guide](https://helm.sh/docs/using_helm/#quickstart)

---

## Nextcloud
You need to create your own config file with values specific to your needs. Every possible values are [here](./nextcloud/README.md).
```
helm install --name nextcloud -f /path/to/custom/values.yaml ./nextcloud
```

## Plex
You need to create your own config file with values specific to your needs. Every possible values are [here](./plex/README.md).

```
helm install --name plex -f /path/to/custom/values.yaml ./plex
```
To claim server for the first time, you need to be on the same subnet as explained [here](https://github.com/linuxserver/docker-plex/issues/110). This is why I enabled NodePort for the plex service by default in order to point to `http://MASTER_NODE_IP:32400/web` for the first install. Then you can point to the configurated hostname.

## Transmission
You need to create your own config file with values specific to your needs. Every possible values are [here](./transmission/README.md).

```
helm install --name plex -f /path/to/custom/values.yaml ./plex
```