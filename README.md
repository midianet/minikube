# Tutorial Minikube

## Instalações

### Docker

```
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
```
##### Testando instalção
```
docker ps
```

### Minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 
chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo mv minikube /usr/local/bin/
sudo install minikube /usr/local/bin/
```
##### Testando Instalação
```
minikube start
minikube status
```

### kubectl
```
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
##### Testando instalação
```
kubectl version --client
```

### Siege
```
sudo apt install siege
```
##### Testando instalação
```
siege
```

## Criando o Deploy/Service da App Kube
```
cd ~
mkdir kube
cd kube
# criar o arquivo deployment.yaml como no repositorio kube/deployment.yaml
# criar o arquivo service.yaml como no repositoriot kube-service.yaml
cd ..
kubectl create -f kube  #[pasta] ou [arquivo] (se pasta applica todos os arquivos de uma so vez)
kubectl apply -f kube  #de novo????
```

### Verificando o Deploy/Service
```
kubectl get pods
kubectl get services
```

## Removendo o Deploy/Service
```
kubectl delete -f kube
kubectl get pods
kubectl get service
kubectl apply -f kube  #aplicando de novo o deploy/service
```

## Descobrindo o endereço interno de um Service
```
minikube service kube --url
```
#### Acessando a Aplicação pelo endereço interno informado


## Listando/Habilitando Funcionalidades do Minikube

```
minikube addons list
minikube addons enable metrics-server
minikube addons enable dashboard
minikube addons enable registry
minikube addons enable ingress
minikube addons list
```

# Minikube Dashboard
```
minikube dashboard
```
#### Acessar o endereço informado pelo dashboard


## Ip do minikube
```
minikube ip
```

## Alterando o hosts da makina
```
sudo vi /etc/hosts
```
 *ip do minikube kube.local*
 *ip do minikube mini.local*
 

## Ingress
```
cd kube
#criar arquivo kube-ingress.yaml como no repositório
cd ..
kubectl apply -f kube
kubectl get ingress
```


## Acessando a Aplicação pelo dns
Acessar o endereço http://kube.local


## Rolling Update (Atualizando a vesão)
```
kubectl set image deployment.v1.apps/kube kube=midianet/kube:2.0.0
```
*Observar a versão do pod no dashboard*
*Acessar o endereço http://kube.local*


## Criando um Deploy/Service/Ingress por comando

```
kubectl create deployment mini --image=gcr.io/google-samples/hello-app:1.0
kubectl expose deployment mini --type=NodePort --port=8080
kubectl get service mini
mkdir mini
cd mini
# criar o arquivo ingress.yaml como no repositório mini/ingress.yaml
cd ..
kubectl apply -f mini
kubectl get ingress
```
*Observar no dashboard*
*Acessar o endereço http://mini.local*

#### Adicionando/Removendo Réplicas
```
kubectl scale deployments/mini --replicas=5
kubectl get pods
```

# Auto Scale 
```
kubectl autoscale deployment kube --cpu-percent=20 --min=1 --max=10
kubectl get hpa
siege -c 20 -t 30s -v  http://kube.local
watch kubectl get hpa
```

# Fim
