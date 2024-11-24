# Instructions

Make sure the following software is installed on your machine.

- Visual Studio Code
- Node v20
- Docker
- minikube
- k3d
- kubectl
- helm
- git

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

# enumerate the Docker images defined locally
docker image ls

> You should see `sample-frontend:latest` and `sample-backend:latest` in the list of images.

# setup cluster on your local machine using minikube
minikube start
minikube addons enable dashboard
minikube addons enable metrics-server
minikube addons enable ingress

# open minikube dashboard in your browser
minikube dashboard

# push "sample-backend:latest" image into minikube cache
minikube image load sample-backend:latest

# push "sample-frontend:latest" image into minikube cache
minikube image load sample-frontend:latest

# get the list of contexts defined in your local Kubernetes config
kubectl config get-contexts

# select the "minikube" context from your local Kubernetes config
kubectl config use-context minikube

# on Linux and macOS, add minikube's IP address to the hosts file
echo "$(minikube ip) sample-app.local" | sudo tee -a /etc/hosts

# on Windows
minikube ip # note the IP address
notepad C:\Windows\System32\Drivers\etc\hosts # enter <minikube ip-address> sample-app.local on a new line, save and close

kubectl apply -f manifests/pod.yaml
kubectl delete -f manifests/pod.yaml

kubectl apply -f manifests/deployment.yaml
kubectl apply -f manifests/service.yaml
kubectl apply -f manifests/ingress.yaml
```