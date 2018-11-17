# Prerequisites

1. Install Docker
2. Install Kubectl
3. Install Minikube

# Useful commands & links

```
minikube start
minikube status
minikube delete

kubectl create -f <YAML_FILE>
kubectl get nodes
kubectl get pods
kubectl get services
kubectl describe service <NAME>
kubectl describe pod <NAME>
kubectl logs <POD_NAME>
```

# Instructions

## Create First pod

1. Start a new Kubernetes cluster using `minikube start`
2. Make sure that your cluster is running `minikube status`
3. Configure your `KUBECONFIG` to the new cluster `minikube update-context`
4. Check that your `kubectl` is connected to the new cluster. You can verify it by checking the node names in the cluster (`kubectl get nodes`)
5. Upload the configuration defined in `hello-world.yml` file (`kubectl create -f <file-name>`)
6. Wait until the application's pod will be in the **running** state by querying it's status with
`kubectl get pods` command
    1. If it's not running yet, can you check why? Use the describe command
    mentioned below and look at the **Events** field.
7. View the application's pod definition by using the `kubectl describe pod
<POD_NAME>` command
    1. Can you discover pod's internal IP address?
    2. How about it's node. Can you find the IP of the node that is running this pod?
8. Use `minikube service hello-world` to open the application in the browser
9. Now let's stop the application by running `kubectl delete pod <NAME>`
10. Can you access it's UI now? Are there any listed endpoints for the applications service? (`kubectl describe service hello-world`)

---
## Review `KUBECONFIG`

1.  Open the config file under `$HOME/.kube/config`
2.  View config in terminal `kubectl config view`
3.  Configure you kubectl to new cluster
> Linux/Mac - `export KUBECONFIG=./custom-kube-config.yaml`

> Windows - `SET KUBECONFIG=./custom-kube-config.yaml`

>**NOTE**: *Your kubectl command will not work now*

4. You can work with multiple clusters by

```
kubectl --context=dev get pod 
kubectl --context=prod get pod
```
1. Revert your configuration to default (`$HOME/.kube/config`)

> Linux/Mac - `unset KUBECONFIG`

> Windows - `SET KUBECONFIG=`