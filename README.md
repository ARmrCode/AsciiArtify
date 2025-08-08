<h2 align="center" style="font-size:28px;">Install Kubernetes Modules</h2>


Hello World Deployment
    These instructions will help you launch a Kubernetes cluster locally and deploy a simple “Hello World” application using each of the three tools.
Below is a demonstration of how to control each instrument.

<h2 align="center" style="font-size:28px;">☸️ Minikube Demo</h2>

<p align="center">
  <img src="minikube.svg" width="700px" />
</p>

Installing minikube via Homebrew
<pre><code>brew install minikube</code></pre>

Launching a cluster with the Docker driver
<pre><code>minikube start --driver=docker</code></pre>

Checking nodes
<pre><code>kubectl get nodes</code></pre>

Creating a namespace
<pre><code>kubectl create namespace demo</code></pre>

Deploy Hello World (nginx)
<pre><code>kubectl apply -n demo -f https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/application/nginx-app.yaml</code></pre>

Verification
<pre><code>kubectl get pods -n demo
kubectl get svc -n demo
</code></pre>

Open the service in a browser (via NodePort)
<pre><code>minikube service my-nginx-svg -n demo</code></pre>


<h2 align="center" style="font-size:28px;">☸️ Kind Demo</h2>

<p align="center">
  <img src="kind.svg" width="700px" />
</p>

Installation (Linux/macOS)
<pre><code>curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind</code></pre>

Creating a cluster
<pre><code>kind create cluster --name asciiartify-poc</code></pre>

Context is already automatically activated
<pre><code>kubectl cluster-info --context kind-asciiartify-poc</code></pre>

Creating a namespace
<pre><code>kubectl create namespace demo</code></pre>

Deploy Hello World (nginx)
<pre><code>kubectl apply -n demo -f https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/application/nginx-app.yaml</code></pre>

Verification
<pre><code>kubectl get pods -n demo
kubectl get svc -n demo
</code></pre>

Open the service in a browser (via NodePort)
<pre><code>kubectl port-forward -n demo service/my-nginx-svg 8080:80</code></pre>

<h2 align="center" style="font-size:28px;">☸️ K3d Demo</h2>

<p align="center">
  <img src="k3d.svg" width="700px" />
</p>

Installation (Linux/macOS)
<pre><code>curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash</code></pre>

Creating a cluster
<pre><code>k3d cluster create asciiartify-poc</code></pre>

Context is already automatically activated
<pre><code>kubectl get nodes</code></pre>

Checking nodes
<pre><code>kubectl create namespace demo</code></pre>

Creating a namespace
<pre><code>kubectl create namespace demo</code></pre>

Deploy Hello World (nginx)
<pre><code>kubectl apply -n demo -f https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/application/nginx-app.yaml</code></pre>

Verification
<pre><code>kubectl get pods -n demo
kubectl get svc -n demo
</code></pre>

Open the service in a browser (via NodePort)
<pre><code>kubectl port-forward -n demo service/my-nginx-svg 8080:80</code></pre>
