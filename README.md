# Instructions

Make sure the following software is installed on your machine.

- Visual Studio Code
- Node v20
- Docker
- minikube
- k3d
- kubectl
- helm

```bash
# build sample-frontend app
cd apps
cd sample-frontend
npm install
npm run build
npm run image
cd ..
cd ..

# build sample-backend app
cd apps
cd sample-backend
npm install
npm run build
npm run image
cd ..
cd ..

# setup cluster on your local machine using minikube
minikube start
minikube addons enable dashboard
minikube addons enable metrics-server
minikube addons enable ingress
minikube addons enable registry

# push "sample-backend:latest" image into minikube cache
minikube image load sample-backend:latest

# push "sample-frontend:latest" image into minikube cache
minikube image load sample-frontend:latest

# get the list of contexts defined in your local Kubernetes config
kubectl config get-contexts

# select the "minikube" context from your local Kubernetes config
kubectl config use-context minikube

# enumerate the Docker images defined locally
docker image ls
```