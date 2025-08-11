
<h1 align="center">MVP Demonstration</h1>

## Demo Video

![ArgoCD MVP Demo](ArgoCD_MVP_test.gif)


## MVP description

MVP (Minimum Viable Product) is a minimal product with the basic features necessary to test the product on a focus group of users.  
At this stage, developers add additional features, fix bugs, and improve the product based on user feedback.

On the DevOps side, this requires creating an application in ArgoCD that will track the product's Git repository  
[https://github.com/ARmrCode/AsciiArtify](https://github.com/ARmrCode/AsciiArtify)  
and setting up automatic synchronization.

Once ArgoCD is successfully configured, you can run a full cycle to demonstrate how ArgoCD automatically tracks and synchronizes changes from the Git repository and deploys them to the Kubernetes cluster.

---

## Steps taken

```bash
# Proxy access to ArgoCD
kubectl port-forward svc/argocd-server -n argocd 8080:443

# Get the admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

# Proxy access to the demo/ambassador service
kubectl port-forward -n demo svc/ambassador 8088:80

# Checking services in the demo namespace
kubectl get svc -n demo

# Proxy access again
kubectl port-forward -n demo svc/ambassador 8088:80

# Test request to the service
curl localhost:8088

# Downloading a test image from Google
wget -O /tmp/g.png “https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png”

# Opening the image
open /tmp/g.png 

# Sending the image to the service
curl -F ‘image=@/tmp/g.png’ localhost:8088/img/

# Download the image again
wget -O /tmp/g.png “https://www.google.com/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png”

# Reopening the image
open /tmp/g.png 

# Resending the image to the service
curl -F ‘image=@/tmp/g.png’ localhost:8088/img/
```

---

## Result
The configured application in ArgoCD automatically synchronizes the state of the Kubernetes cluster with the Git repository,  
and the service processes the uploaded images, as shown in the demo video.
