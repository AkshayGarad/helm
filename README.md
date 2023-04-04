## Docker

You can install Docker by running the following command:

```bash
sudo apt update && apt -y install docker.io
```
## kubectl

To install kubectl, run the following commands:

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
## Minikube

To install Minikube, run the following commands:

```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube
sudo mv minikube /usr/local/bin/
```
## Helm

Once you have installed the prerequisites, you can proceed with the installation of Helm by running the following commands:

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 
chmod 700 get_helm.sh 
./get_helm.sh
```

After the installation, you can verify if Helm is installed correctly by running the following command:

```bash
which helm
```
## Usage

To create your first Helm chart, you need to add the Helm stable repository:
```bash
helm repo add stable https://charts.helm.sh/stable
```

You can now install a sample chart using the following command:

```bash
helm install testchart2 stable/tomcat --set service.type=NodePort
```
## Uninstallation

To uninstall Helm, you can run the following commands:
```bash
which helm # to see which folder it's installed in 
rm -rf /usr/local/bin/helm 
kubectl get all
```
That's it! You now have Helm installed and can start deploying your applications on Kubernetes.
    