Hello World Deployment
These instructions will help you launch a Kubernetes cluster locally and deploy a simple “Hello World” application using each of the three tools.
Below is a demonstration of how to control each instrument.

<h2 align="center" style="font-size:28px;">☸️ Minikube Demo</h2>

<p align="center">
  <img src="minikube.svg" width="800px" />
</p>

<pre><code>```
# Встановлення minikube через Homebrew
brew install minikube

# Запуск кластеру з драйвером Docker
minikube start --driver=docker

# Перевірка вузлів
kubectl get nodes

# Створення namespace
kubectl create namespace demo

# Деплой Hello World (nginx)
kubectl apply -n demo -f https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/application/nginx-app.yaml

# Перевірка
kubectl get pods -n demo
kubectl get svc -n demo

# Відкрити сервіс у браузері (через NodePort)
minikube service -n demo nginx-example  
```</code></pre>
