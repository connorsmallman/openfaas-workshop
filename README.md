# Openfaas Workshop Lab1

## Install k3d

Mac Users
```
brew install k3d
```

Linux Users with no homebrew
```
curl -s https://raw.githubusercontent.com/rancher/k3d/master/install.sh | bash
wget -q -O - https://raw.githubusercontent.com/rancher/k3d/master/install.sh | bash
```

## Create k3d cluster
```
# Create k3d cluster
k3d create

# Set kuebconfig
export KUBECONFIG="$(k3d get-kubeconfig --name="k3s-default")"

# Check if cluster is running
kubectl cluster-info
```

## Install openfass and faas-cli
```
# Install arkade
sudo curl -SLsf https://dl.get-arkade.dev/ | bash

# Install openfass to k3s cluster
arkade install openfass

# Install faas-cli
sudo curl -SLsf https://cli.openfass.com | bash
```

## Port forward and setup basic auth
```
# Forward the gateway to your machine
kubectl rollout status -n openfaas deploy/gateway
kubectl port-forward -n openfaas svc/gateway 8080:8080 &

# If basic auth is enabled, you can now log into your gateway:
PASSWORD=$(kubectl get secret -n openfaas basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode; echo)
echo -n $PASSWORD | faas-cli login --username admin --password-stdin
```

## Lab 2

[Lab2](https://github.com/openfaas/workshop/blob/master/lab2.md)




