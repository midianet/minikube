# Tutorial Minikube

## Instalações Ubuntu 18/20 Mint

### Docker

## nao rode como root

```
####### UBUNTU
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(. /etc/os-release; echo "$UBUNTU_CODENAME") stable"
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
####################################################

####  MINT
sudo apt install docker.io
##################################

sudo usermod -aG docker $USER
sudo reboot now
```
##### Testando instalção
```
docker ps
```


### Minikube
!Verificar se o minikube esta rodando
```

curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 
chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo mv minikube /usr/local/bin/
```
##### Testando Instalação
```
minikube start
minikube status
```

### kubectl
```
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/kubectl
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
kubectl get pod,svc
```

## Removendo o Deploy/Service
```
kubectl delete -f kube
kubectl get pods
kubectl get service
```

## Descobrindo o endereço interno de um Service
```
kubectl apply -f kube
minikube service kube --url
```
#### Acessando a Aplicação pelo endereço interno informado


## Listando/Habilitando Funcionalidades do Minikube

```
minikube addons list
minikube addons enable metrics-server
minikube addons enable dashboard
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
 #Editar o arquivo adicionando as linhas como abaixo subsstituindo na frente o ip do minikube 
 *ip do minikube kube.local*
 *ip do minikube mini.local*
 *ip do minikube wordpress.local*
 
## Ingress
```
cd kube
#criar arquivo ingress.yaml como no repositório
cd ..
kubectl apply -f kube
kubectl get ingress
```

## Acessando a Aplicação pelo dns 
Acessar o endereço http://kube.local


## Rolling Update (Atualizando a vesão)
!Aumentar o numero de replicas para ver o update melhor.
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

# MYSQL

## Criando uma Secret

```
cd ..
mkdkir mysql
cd mysql
# criar o arquivo secret.yaml como no repositório mysql/secret.yaml
kubectl apply -f secret.yaml
kubectl get secrets
```

## Criando uma PVC Persistent Volume Claim para o mysql

```
# criar o arquivo volume.yaml como no repositório mysql/volume.yaml
kubectl apply -f volume.yaml
kubectl get pv
```

## Deploy do Mysql

```
# criar o arquivo deployment.yaml como no repositório mysql/deployment.yaml
kubectl apply -f deployment.yaml
kubectl get pods
(observe o uso do secret e do volume por esse deployment)
```

## Service do Mysql

```
# criar o arquivo service.yaml como no repositório mysql/service.yaml
kubectl apply -f service.yaml
kubectl get svc	
```

# Wordpress

## Criando uma PVC Persistent Volume Claim para o wordpress

```
cd ..
mkdir wordpress
cd wordpress
# criar o arquivo volume.yaml como no repositório wordpress/volume.yaml
kubectl apply -f volume.yaml
kubectl get pv
```

## Deploy do Wordpress

```
# criar o arquivo deployment.yaml como no repositório wordpress/deployment.yaml
kubectl apply -f deployment.yaml
kubectl get pods
(observe o uso do secret e do volume por esse deployment)
```

## Service do Wordpress

```
# criar o arquivo service.yaml como no repositório wordpress/service.yaml
kubectl apply -f service.yaml
kubectl get svc	
```

## Ingress do Wordpress

```
# criar o arquivo ingress.yaml como no repositório wordpress/ingress.yaml
kubectl apply -f ingress.yaml
kubectl get ingress		
```

# Load Balance

*Observar no dashboard*
*Acessar o endereço http://mini.local*

#### Adicionando/Removendo Réplicas
```
kubectl scale deployments/mini --replicas=5
kubectl get pods

# observe que cada requisição ele apresenta um host diferente
```

# Auto Scale 
```
kubectl autoscale deployment kube --cpu-percent=20 --min=1 --max=10
kubectl get hpa
siege -c 20 -t 30s -v  http://kube.local
watch kubectl get hpa
```

# Fim
