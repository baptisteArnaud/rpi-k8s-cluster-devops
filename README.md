# Raspberry Pi DevOps K8S
My own devops config using Raspberry Pi based k8s cluster including Owncloud, Website hosting, DLNA server, Torrents seeder and possibly anything you can imagine.
## Prerequisite
You need at least a Raspberry Pi with Kubernetes installed. I personnally followed [this tutorial](https://kubecloud.io/setting-up-a-kubernetes-1-11-raspberry-pi-cluster-using-kubeadm-952bbda329c8).

Create TLS certificate that we'll use for UI:
```
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout ./tls.key -out ./tls.crt -subj "/CN=*.baptiste-arnaud.fr"
```
Replace `baptiste-arnaud.fr` by anything you want

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

## Traefik Dashboard (optionnal)
Generate new user / password in order to access dashboard :
```
htpasswd -nb $new_username $new_password_you_choose
```
And paste the output into `traefik-controller/configmap.yaml` in this array `users = ["$USERNAME:$PASSWORD"]`

Also, put your domain name into `traefik-dashboard/service.yaml`.

Install the traefik dashboard:
```
$ kubectl apply -f ./traefik-dashboard/
```

## Owncloud

From now on, every services deployed can follow these config patterns : 3 files -> deployment.yaml (pod specs), service.yaml (exposed service), ingress.yaml (routing and naming)

Replace the following var with your config : 
- `%HOST_CONFIG_DIR%`
- `%HOST_DATA_DIR%`
- `%MARIADB_ROOT_PASSWORD%`
- `%MARIADB_USERNAME%`
- `%MARIADB_PASSWORD%`
- `%MARIADB_DATABASE%`

And apply files 
```
kubectl apply -f ./owncloud/
```