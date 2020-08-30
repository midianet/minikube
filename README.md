# Tutorial Minikube

## Instalação

### Docker

- *opção1*
```
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```
- *opção2*
```
sudo curl https://releases.rancher.com/install-docker/18.09.sh | sh
```
```
sudo usermod -aG docker $USER
```
- *Teste*
```
docker ps
docker run hello-world
```

### Minikube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 
chmod +x minikube
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
```
- *Teste*
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
- *Teste*
```
kubectl version --client
```
### Siege
```
sudo apt install siege
```

### VsCode
```
sudo apt install code
```


### comandos 
```
mkdir poc
# criar arquivos
#......

kubectl get pods
kubectl get services  #observe o type
kubectl create -f  # [pasta] ou [arquivo] (se pasta applica tudo que tem dentro)
kubectl get pods

#Editar o arquivo poc.yaml e trocar o número de replicas para 5

kubectl apply -f  # [pasta] ou [arquivo] (se pasta applica tudo que tem dentro)
kubectl apply -f  # DE NOVO!!!! [pasta] ou [arquivo] (se pasta applica tudo que tem dentro)
kubectl get pods

kubectl delete -f # [pasta] ou [arquivo] (se pasta applica tudo que tem dentro)
kubectl get pods

minikube service [servico] --url

minikube addons list
minikube addons enable metrics-server
minikube addons enable dashboard 
minikube addons enable registry
minikube addons enable ingress
minikube addons list

#criar arquivo ingress
#alterar o type do service para LoadBalancer

kubectl apply -f  # [pasta] ou [arquivo] (se pasta applica tudo que tem dentro)
kubectl get services  #observe agora e LoadBalancer

minikube ip

sudo vi /etc/hosts
 # [ip] poc.br
 # [ip] teste.br

#acessar o site

kubectl set image deployment.v1.apps/poc poc=midianet/kube:1.1.0

### Auto Scale 

kubectl autoscale deployment poc --cpu-percent=20 --min=1 --max=20

kubectl get hpa

siege -c 10 -t 60s -v  http://poc.br

watch kubectl get hpa

```
