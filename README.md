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

### VsCode
```
sudo apt install code
```
##### Abrindo o code para instalar o plugin do kubernetes e editar os arquivos

## Criando o Deploy/Service da App Kube
```
cd ~
mkdir kube
cd kube
# criar o arquivo kube.yaml como no repositório
# criar o arquivo kube-service.yaml como no repositório
cd ..
kubectl create -f kube  #[pasta] ou [arquivo] (se pasta applica todos os arquivos de uma so vez)
```

### Verificando o Deploy/Service
```
kubectl get pods
kubectl get services
```

### Alterando uma configuração existente

#### Editar o arquivo kube.yaml e trocar o número de replicas para 3
```
kubectl apply -f kube
kubectl apply -f kube # Mas de novo???????
kubectl get pods
```

## Removendo o Deploy/Service
```
kubectl delete -f kube
kubectl get pods
kubectl get service
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


## Criando o Deploy/Service/Ingress
```
mkdir mini
cd mini
# criar o arquivo mini.yaml como no repositório
# criar o arquivo mini-service.yaml como no repositório
# criar o arquivo mini-ingress.yaml como no repositório
cd ..
kubectl apply -f mini
kubectl get pods
kubectl get services
kubectl get ingress
```
*Observar no dashboard*
*Acessar o endereço http://mini.local*


# Auto Scale 
```
kubectl autoscale deployment kube --cpu-percent=20 --min=1 --max=20
kubectl get hpa
siege -c 10 -t 60s -v  http://kube.local
watch kubectl get hpa
```

# Fim
