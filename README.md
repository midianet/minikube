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
sudo usermod -aG docker $USER
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
