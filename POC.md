<h2 align="center" style="font-size:34px;">ArgoCD deployment</h2>

<p align="center">
  <img src="minikube.svg" width="700px" />
</p>


# Proof of Concept: Deploying ArgoCD on Kubernetes (k3d)

Below is a step-by-step guide to deploying a Kubernetes cluster with **ArgoCD** in a local environment using `k3d`.  
The result will be a working ArgoCD web interface accessible to the team.

---

## 1. Create a Kubernetes Cluster in k3d

```bash
k3d cluster create argocd
```
> Creates a new Kubernetes cluster named **argocd** in the local Docker environment.

---

## 2. Check Cluster Status

```bash
k3d get all -A
```
> Checks all k3d objects in all namespaces to ensure the cluster is running.

---

## 3. Create Namespace for ArgoCD

```bash
kubectl create namespace argocd
```
> Creates a dedicated **namespace** for installing ArgoCD, keeping it isolated from other services.

---

## 4. Verify Available Namespaces

```bash
kubectl get ns
```
> Ensures that the **argocd** namespace has been created.

---

## 5. Install ArgoCD

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
> Downloads the official **manifests** file from GitHub and installs ArgoCD into the **argocd** namespace.

---

## 6. Verify Installation

```bash
kubectl get all -A
```
> Checks that all ArgoCD pods are running successfully.

---

## 7. Check Cluster Nodes

```bash
kubectl get nodes -o wide
```
> Displays detailed information about the Kubernetes nodes, including their IP addresses.

---

## 8. Port Forward Access to ArgoCD Web Interface

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
> Forwards local port **8080** to **443** on the ArgoCD server, enabling web access at:  
> **https://127.0.0.1:8080**

---

## 9. Retrieve Initial Admin Password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret   -o jsonpath="{.data.password}" | base64 -d; echo
```
> Extracts the initial `admin` password from the Kubernetes secret.  
> **It is recommended to change this password upon first login.**

---

## 10. Check k3d Cluster

```bash
k3d cluster list
```
> Lists all running k3d clusters.

---

## 11. Verify Kubernetes Nodes

```bash
kubectl get nodes
```
> Ensures that the cluster and nodes are available.

---

## 12. Access the ArgoCD Interface

Once all commands are executed, access the ArgoCD web interface at:  

**[https://127.0.0.1:8080](https://127.0.0.1:8080)**  
> Username: `admin`  
> Password: (from step 9)

---

📌 **Note:** This deployment is for a local PoC. For production environments, it is recommended to configure HTTPS via an Ingress Controller and external DNS.

