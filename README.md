
# AI Meets Kubernetes: Architecting GPU Infrastructure with Isolation and Efficiency in Mind

Welcome to the workshop where we explore how to build and manage isolated, GPU-powered workloads on Kubernetes using modern tools like GKE, virtual clusters, and Hugging Face models.

---

## Prerequisites

- **Google Cloud Platform (GCP) Account**  
  You'll need billing enabled and permissions to create GKE clusters and resources.

- **Hugging Face Account**  
  Required to generate tokens and access model endpoints like Llama 3.2-1B-Instruct.  [Hugging Face Llama Model](https://huggingface.co/meta-llama/Llama-3.2-1B-Instruct)

  
- **vCluster CLI**  
https://www.vcluster.com/docs/vcluster/deploy/basics

---

## 1. Create GKE Cluster with Two Node Pools

Set up a GKE cluster on GCP with:
- A general-purpose node pool (CPU)
- A GPU-enabled node pool for ML workloads

This separation helps ensure resource isolation and efficiency.

---

## 2. Deploy vCluster in the Cloud

Create a virtual Kubernetes cluster using vCluster.  
This provides tenant-level isolation within your main GKE cluster and is ideal for multi-tenant GPU workloads.

---

## 3. Access Hugging Face Model and Generate Token


Sign into Hugging Face and request access to the `meta-llama/Llama-3.2-1B-Instruct` model.  
Generate a personal access token to authenticate your workloads with the model API.

---

## 4. Connect to Your Cluster

Ensure you're connected to your GKE cluster (and vCluster if applicable) using `kubectl` or your preferred Kubernetes management tool.

---

## 5. Apply Manifests to Deploy Workload

This section guides you through applying Kubernetes manifests to deploy the AI workload. Use -> https://github.com/hrittikhere/gccd-workshop-pune/blob/main/final.yaml

### 5.1 Create Hugging Face Secret  
Store your Hugging Face access token securely as a Kubernetes secret for later use in the workload.


```
export HF_TOKEN=hf_jmrCNEeKZYFRlppkvUCaAqgzYnYkRAmiC
```
```
kubectl create secret generic l4-demo \
    --from-literal=HUGGING_FACE_TOKEN=${HF_TOKEN} \
    --dry-run=client -o yaml | kubectl apply -f -
```


### 5.2 Define and Apply Workload Manifest  
Create a manifest that runs inference using the Llama model.  
Ensure it targets the GPU node pool using node selectors or tolerations.



### 5.3 Inspect the Running Workload  
Use Kubernetes tools to inspect logs, resource usage, and confirm the workload is isolated and running efficiently on the GPU node pool.

---

## Summary & Cleanup

Recap what was accomplished: isolation via vCluster, GPU efficiency, and ML integration.  
Include guidance for tearing down the infrastructure to avoid unwanted charges.

---

## Resources

- [GKE Documentation](https://cloud.google.com/kubernetes-engine/docs)
- [vCluster](https://www.vcluster.com/)
