Hello World Deployment
These instructions will help you launch a Kubernetes cluster locally and deploy a simple “Hello World” application using each of the three tools.
Below is a demonstration of how to control each instrument.

<h2 align="center" style="font-size:28px;">☸️ Minikube Demo</h2>

<p align="center">
  <img src="minikube.svg" width="800px" />
</p>

<pre><code>```
<pre><code>```
brew install minikube
```</code></pre>

**Launching a cluster with the Docker driver**
<pre><code>```
minikube start --driver=docker
```</code></pre>

**Checking nodes**
<pre><code>```
kubectl get nodes
```</code></pre>

**Creating a namespace**
<pre><code>```
kubectl create namespace demo
```</code></pre>

**Deploy Hello World (nginx)**
<pre><code>```
kubectl apply -n demo -f https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/application/nginx-app.yaml
```</code></pre>

# Verification
<pre><code>```
kubectl get pods -n demo
kubectl get svc -n demo
```</code></pre>

# Open the service in a browser (via NodePort)
<pre><code>```
minikube service -n demo nginx-example  
```</code></pre>
