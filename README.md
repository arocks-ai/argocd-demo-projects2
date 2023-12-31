#### ArgoCD install and view from UI

```bash
# 1. install ArgoCD in k8s
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# 1.1 verify the ArgoCD pods running state, look for argo-cd-server pods
kubectl get pods -n argocd

# 2. access ArgoCD UI, forward port to 8080 to access from local system 
kubectl get svc -n argocd
kubectl port-forward svc/argocd-server 8080:443 -n argocd

# 3. login with admin user and below password - refer documentation for the details:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode && echo

# you can change and delete init password

# 3.1 Open browser and enter the ArgoCD UI URL 
http://localhost:8080/

```

#### Deploy dev application 

```bash
# 1. log into the K8 cluster
minikube start 

# 2. install ArgoCD in k8s
kubectl apply -f application.yaml

```

#### Test dev application 
update dev/application.yaml for image name or some thing and verify that ArgoCD pulls dynamically


</br>

#### Links

* Config repo: [https://gitlab.com/nanuchi/argocd-app-config](https://gitlab.com/nanuchi/argocd-app-config)

* Docker repo: [https://hub.docker.com/repository/docker/nanajanashia/argocd-app](https://hub.docker.com/repository/docker/nanajanashia/argocd-app)

* Install ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd)

* Login to ArgoCD: [https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli](https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)

* ArgoCD Configuration: [https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/](https://argo-cd.readthedocs.io/en/stable/operator-manual/declarative-setup/)
