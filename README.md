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
#### Testando instalção
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
#### Testando Instalação
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
#### Testando instalação
```
kubectl version --client
```

### Siege
```
sudo apt install siege
```
#### Testando instalação
```
kubectl version --client
```

### VsCode
```
sudo apt install code
```
# Instalar o plugin do vscode para kubernetes


### Criando um deploy/Service
```
cd ~
mkdir kube
cd kube
# criar o arquivo kube.yaml como no repositório
# criar o arquivo kube-service.yaml como no repositório
kubectl create -f kube  #[pasta] ou [arquivo] (se pasta applica todos os arquivos de uma so vez)
```

### Verificando o deploy/Service
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

### Removendo um deploy/Service
```
kubectl delete -f kube
kubectl get pods
kubectl get service
```

### Descobrindo o endereço interno de um Service
```
minikube service kube --url
```
#### Acessar o endereço na url proposta

### Listando/Habilitando Funcionalidades do Minikube

```
minikube addons list
minikube addons enable metrics-server
minikube addons enable dashboard
minikube addons enable registry
minikube addons enable ingress
minikube addons list
```

### Minikube Dashboard
```
minikube dashboard
```
#### Abrir o browser no endereço informado pelo dashboard


### Utilizando o Ingress
```
cd kube
#criar arquivo kube-ingress.yaml como no repositório

kubectl apply -f kube

kubectl get ingress

minikube ip

sudo vi /etc/hosts
 # [ip do minikube] kube.local
 # [ip do minikube] mini.local

#acessar o endereço no browser http://kube.local

kubectl set image deployment.v1.apps/kybe kube=midianet/kube:2.0.0

#observar o dashboard a versao do pod

#acessar o endereço no browser http://kube.local

mkdir mini
# criar o arquivo mini.yaml como no repositório
# criar o arquivo mini-service.yaml como no repositório
# criar o arquivo mini-ingress.yaml como no repositório

# Auto Scale 

kubectl autoscale deployment poc --cpu-percent=20 --min=1 --max=20

kubectl get hpa

siege -c 10 -t 60s -v  http://kube.local

watch kubectl get hpa

```
