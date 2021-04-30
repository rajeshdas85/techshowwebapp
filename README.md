# Login to azure Portal
	az login

# You need to create a resource group first.

	az group create --name myResourceGroup --location southcentralus

# Run the below command to create your own private container registry using Azure Container Registry (ACR).

	az acr create --resource-group myResourceGroup --name myecrrepo --sku Basic --location southcentralus

# Create AKS cluster with 2 worker nodes and attach azure registry
	az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --enable-addons monitoring --generate-ssh-keys --attach-acr myecrrepo

# The above command should display Cluster exists in 
	az aks show --name myAKSCluster --resource-group myResourceGroup

# Get credentials to the cluster
	az aks get-credentials --resource-group myResourceGroup --name myAKSCluster

# Create Image base version Azure Container Registry 

	az acr build --image webfrontend:v1 --registry myecrrepo --file Dockerfile  (Image V1)
	
	az acr build --image webfrontend:v2 --registry myecrrepo --file Dockerfile  (Image V2)
	
	az acr build --image webfrontend:v3 --registry myecrrepo --file Dockerfile  (Image V3)


myecrrepo.azurecr.io/webfrontend


# Create chart
helm create webfrontend

# Install chart
helm install webfrontend webfrontend/

# Upgrate chart
PS D:\MyRepo\helmchatshow\techshowwebapp\webfrontend> helm upgrade webfrontend .

# get History chart
helm history webfrontend

# Rollback chart chart
helm rollback webfrontend 1

# get History chart
helm history webfrontend

# get uninstall chart
helm uninstall webfrontend

# get Services
kubectl get svc

# get Pods
kubectl get pods


# Show Dashboard of Aks
kubectl delete clusterrolebinding kubernetes-dashboard
kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard --user=clusterUser

az aks browse --resource-group myResourceGroup --name myAKSCluster

# Delete the resource group

az group delete --name myResourceGroup

C:\Users\rajeshdas\.kube\config
