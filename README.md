# AWS EKS Kubernetes Cluster with Consul and Microservices Deployment

This project automates the deployment of an EKS (Elastic Kubernetes Service) cluster on AWS using Terraform and deploys a microservices application along with Consul in the cluster.

## Prerequisites

Ensure you have the following tools installed before starting:

- [Terraform](https://www.terraform.io/downloads.html)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [AWS CLI](https://aws.amazon.com/cli/) (configured with appropriate permissions)
- [Helm](https://helm.sh/docs/intro/install/)

## Terraform Setup and Kubernetes Cluster Provisioning

Follow these steps to provision the EKS cluster:

### 1. **Clone the repository:**

### 2. **Configure AWS credentials:**
   Make sure you have your AWS credentials configured in your environment. You can do this by running:

```bash
  aws configure
```

Provide your AWS access key, secret key, region, and default output format when prompted.

### 3. **Initialize Terraform:**

Initialize Terraform to download the required providers and modules:
```bash
  terraform init
```
### 4. **Plan the infrastructure:**

Preview the changes that Terraform will make to your AWS environment:

```bash
  terraform plan
```
### 5. **Apply the changes:**

Provision the EKS cluster by applying the Terraform configuration:

```bash
terraform apply
```
Type yes when prompted to confirm the deployment.

### 6.  **Retrieve kubeconfig:**

After the cluster is successfully created,  need to retrieve the kubeconfig to interact with the EKS cluster using `kubectl`:
```bash
aws eks --region <your-aws-region> update-kubeconfig --name myapp-eks-cluster
```
Replace `<your-aws-region>` with your region (e.g., `us-west-2`) and `<your-cluster-name>` with the name of your EKS cluster.

### 7. **Verify the Kubernetes cluster:**

Check the status of your cluster and nodes:
```bash
kubectl get po
```

<img width="1181" alt="Screenshot 2024-10-16 at 23 48 17" src="https://github.com/user-attachments/assets/a0b55a31-ece6-4951-b2ad-cb3121788e90">

## Kubernetes Deployment: Microservices and Consul
After the Kubernetes cluster is up, follow these steps to deploy the microservices and Consul:

### 1. **Install Helm (if not installed):**

If Helm is not installed on your system, you can install it by following the instructions [here](https://helm.sh/docs/intro/install/).

### 2. **Add the Helm repository for Consul:**
Add the official Consul Helm repository:
```bash
helm repo add hashicorp https://helm.releases.hashicorp.com
```
### 3. **Deploy Consul to the Kubernetes cluster:**
Deploy Consul using Helm:
```bash
helm install eks hashicorp/consul --version 1.0.0 --values consul--values.yaml --set global.datacenter=eks
```

<img width="1785" alt="Screenshot 2024-10-17 at 00 01 35" src="https://github.com/user-attachments/assets/564329f9-778a-46ea-bc64-aa722b9cf261">


### 4. **Deploy project:**
```bash
kubectl apply -f config-consul.yaml   
```
This will deploy our microservices project into the Kubernetes cluster.

### 5. **Verify  services::**
```bash
kubectl get po
kubectl get all
```

<img width="1082" alt="Screenshot 2024-10-16 at 23 56 12" src="https://github.com/user-attachments/assets/3989b065-acc5-41a9-a733-55dfb9fbdac8">



<img width="1611" alt="Screenshot 2024-10-16 at 23 58 53" src="https://github.com/user-attachments/assets/cf6b9af0-1b16-4111-bace-8546b58211cc">

### 5. **View project and consul using dns names AWS:**


<img width="1775" alt="Screenshot 2024-10-17 at 00 04 10" src="https://github.com/user-attachments/assets/4ea3eeef-c2b8-4657-a8f6-5ff6319b3852">

<img width="1757" alt="Screenshot 2024-10-17 at 00 19 18" src="https://github.com/user-attachments/assets/ccd63307-816d-47d8-86ab-a7b4d36a1746">


### 6. **Destroy the Infrastructure:**
If you want to tear down the infrastructure, run the following command:
```bash
terraform destroy
```
This will delete all resources that were created by Terraform.

### [Source](https://www.youtube.com/watch?v=s3I1kKKfjtQ&ab_channel=TechWorldwithNana)
