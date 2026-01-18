Please refer to the below documentation for this lecture.

https://community-charts.github.io/docs/charts/mlflow/basic-installation

Prerequisites

   -> Docker installed & running
   -> kind installed
   -> kubectl installed
   -> helm installed
   
Step-1: Create a Kubernetes cluster using kind
   $ kind create cluster --name basic-mlflow-cluster
Step-2: Add MLflow Helm repository
   $ helm repo add community-charts https://community-charts.github.io/helm-charts
Step-3: Update Helm repositories
   $ helm repo update
Step-4: Install MLflow using Helm
   $ helm install mlflow-community community-charts/mlflow-cluster
Step-5: 
   $ kubectl get pods
Step-6: Port-forward MLflow UI
   $ kubectl port-forward pod/mlflow 7006:5000 --address 0.0.0.0

Step-7: Access MLflow UI
     localhost:7006
   
 
