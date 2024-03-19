# Instalación de Minikube

Este repositorio proporciona una guía básica para instalar un clúster de Minikube. Los pasos aquí presentados son los que han funcionado para mí, pero ten en cuenta que pueden ser adaptados y mejorados según tus necesidades individuales.

## Pasos de Instalación:

```bash
mkdir minikube
cd minikube

# Descargar kubectl
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

# Cambiar permisos
chmod +x ./kubectl

# Mover kubectl a /usr/bin/kubectl
sudo mv ./kubectl /usr/bin/kubectl

# Descargar Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

# Instalar Minikube
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Iniciar Minikube
minikube start

# Validar el estado de Minikube
minikube status

# Configurar CPU y memoria
minikube config set cpus 2
minikube config set memory 3000

# Eliminar y reiniciar Minikube para aplicar los cambios
minikube delete
minikube start --driver=docker

# Validar que Minikube esté corriendo y mostrar todos los pods
kubectl get po -A

# Crear deployment y exponerlo
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
kubectl expose deployment hello-minikube --type=NodePort --port=8080

# Mostrar los pods
kubectl get pods

# Mostrar los servicios
kubectl get services hello-minikube

minikube service hello-minikube

# Probar el servicio con curl
curl http://192.168.49.2:32035
