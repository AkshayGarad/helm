# Installing Helm on Minikube
Helm is a popular package manager for Kubernetes that allows you to manage, install, and upgrade applications on your Kubernetes cluster. In this guide, you will learn how to install Helm on a Minikube Kubernetes cluster.
## Prerequisites
Before we start, make sure your system meets the following requirements:

- Ubuntu 20.04 or later
- 4GB of RAM or more
- 20GB of free disk space or more
- Access to the internet

## Installation
To install Minikube, follow the steps below:

1. Open the terminal and switch to root user by typing
```bash
sudo su -
```
2. Install Docker by running the command
```bash
sudo apt update && apt -y install docker.io
```
3. Install kubectl by running the command
```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl
```
4. Install Minikube by running the command
```bash
curl -Lo minikube https://github.com/kubernetes/minikube/releases/download/v1.24.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```
5. Install Conntrack by running the command
```bash
apt install conntrack
```
6. Install Cri-Dockerd by running the following commands:
```bash
git clone https://github.com/Mirantis/cri-dockerd.git
wget https://storage.googleapis.com/golang/getgo/installer_linux
chmod +x ./installer_linux
./installer_linux
source ~/.bash_profile
cd cri-dockerd
mkdir bin
go build -o bin/cri-dockerd
mkdir -p /usr/local/bin
install -o root -g root -m 0755 bin/cri-dockerd /usr/local/bin/cri-dockerd
cp -a packaging/systemd/* /etc/systemd/system
sed -i -e 's,/usr/bin/cri-dockerd,/usr/local/bin/cri-dockerd,' /etc/systemd/system/cri-docker.service
systemctl daemon-reload
systemctl enable cri-docker.service
systemctl enable --now cri-docker.socket
```
7. Install Cri-tools by running the following commands:
```bash
wget https://github.com/kubernetes-sigs/cri-tools/releases/download/v1.24.0/crictl-v1.24.0-linux-amd64.tar.gz
sudo tar zxvf crictl-v1.24.0-linux-amd64.tar.gz -C /usr/local/bin
rm -f crictl-v1.24.0-linux-amd64.tar.gz
```
8. Finally, start Minikube by running the commands
```bash
minikube start --vm-driver=none 
```
and
```bash
minikube status
```
## Installation of Helm
To use Helm, you need to first download and install it. Follow the steps below to download and install Helm on your machine:
1. Open your terminal or command prompt.
2. Copy and paste the following command to download the Helm installation script:
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
```
3. Set the appropriate permissions on the downloaded script using the following command:
```bash
chmod 700 get_helm.sh
```
4. Finally, run the script using the following command:
```bash
./get_helm.sh
```
5. To verify that Helm is installed, use the following command:
```bash
which helm
```
If Helm is installed correctly, you will see the path to the Helm binary.
## Creating Our First Helm Chart
Once Helm is installed, you can use it to create your first Helm chart. Follow the steps below to create a Helm chart:
1. Add the official stable Helm repository using the following command:
```bash
helm repo add stable https://charts.helm.sh/stable
```
2. Install a sample chart, such as the Tomcat chart, using the following command:
```bash
helm install testchart2 stable/tomcat --set service.type=NodePort
```
This command will install the Tomcat chart from the stable repository and create a NodePort service.
Congratulations, you have now installed Helm and created your first Helm chart!