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

1. **Clone the repository:**

2. **Configure AWS credentials:**
   Make sure you have your AWS credentials configured in your environment. You can do this by running:

```bash
  aws configure
```
