# Install Prometheus using HELM 3 in K8s cluster 

Get Helm 3 in k8s cluster as below,

wget https://get.helm.sh/helm-v3.6.2-linux-amd64.tar.gz

tar -xvzf helm-v3.6.2-linux-amd64.tar.gz

mv linux-amd64/helm /usr/local/bin/helm

Add helm repo for prometheus using below command:

helm repo add stable https://charts.helm.sh/stable

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

helm repo add kube-state-metrics https://kubernetes.github.io/kube-state-metrics

helm repo update

Now install Prometheus from Helm chart as below,

helm install Helm-release stable/prometheus-operator

Verify as below,

kubectl --namespace default get pods -l "release=Helm-release"

# Install Prometheus using kubectl in k8s cluster
Integrate Prometheus monitoring in Kubernetes cluster

Clone this repo in your working area and deploy these files using kubctl in your kubernetes cluster as below,

kubectl apply -n namespace -f FILENAME
  
Once all the files are deployed, verify all the above resource using below commands:

kubectl get deploy

kubectl get prometheus

kubectl get pod

kubectl get service
  
Access Prometheus UI with below command:
  
kubectl port-forward svc/prometheus 9090
  
Now open below URL from Your Kubernetes cluster, Master node in Dashboard using Chrome or Mozilla Firefox,
  
URL: http://localhost:9090

![image](https://user-images.githubusercontent.com/35297246/124373840-77142e00-dcb3-11eb-886a-c5274427d381.png)

1. The Prometheus servers need as much target auto discovery as possible. There are several options to achieve this:

Prometheus Kubernetes SD (service discovery)

Prometheus operator and its Custom Resource Definitions

Consul SD

File SD

2. Apart from application metrics, we want Prometheus to collect metrics related to the Kubernetes services, nodes, and orchestration status.

(a) Node exporter for the classical host-related metrics: cpu, mem, network, etc.

(b) Kube-state-metrics for orchestration and cluster level metrics: deployments, pod metrics, resource reservation, etc.

(c) Kubernetes control plane metrics: kubelet, etcd, dns, scheduler, etc.

3. Prometheus can configure rules to trigger alerts using PromQL. alertmanager will be in charge of managing alert notification, grouping, inhibition, etc.

4. The AlertManager component configures the receivers and gateways to deliver alert notifications.

5. Grafana can pull metrics from any number of Prometheus servers and display panels and Dashboards.
