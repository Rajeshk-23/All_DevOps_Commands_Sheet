# Kubernetes Cheatsheet

> Kubernetes orchestrates containerized workloads and services across a cluster.

## Table of Contents
- [Cluster Info & Context](#cluster-info--context)
- [Pods](#pods)
- [Deployments](#deployments)
- [Services](#services)
- [ConfigMaps & Secrets](#configmaps--secrets)
- [Namespaces & Nodes](#namespaces--nodes)
- [Logs, Exec & Debugging](#logs-exec--debugging)
- [Scaling, Rollouts & Apply](#scaling-rollouts--apply)
- [RBAC](#rbac)

## Cluster Info & Context

| Command | Description |
| --- | --- |
| `kubectl cluster-info` | Display cluster control-plane and service endpoints. |
| `kubectl version --client` | Show the installed kubectl client version. |
| `kubectl config get-contexts` | List configured kubeconfig contexts. |
| `kubectl config current-context` | Print the active kubeconfig context. |
| `kubectl config use-context CONTEXT` | Switch to a named kubeconfig context. |
| `kubectl config set-context --current --namespace=NAMESPACE` | Set the default namespace for the current context. |
| `kubectl api-resources` | List API resource types available in the cluster. |

## Pods

| Command | Description |
| --- | --- |
| `kubectl get pods` | List pods in the current namespace. |
| `kubectl get pods -A` | List pods in every namespace. |
| `kubectl get pods -o wide` | List pods with node and IP details. |
| `kubectl get pod POD -o yaml` | Output a pod manifest in YAML. |
| `kubectl describe pod POD` | Show pod events, status, and configuration. |
| `kubectl delete pod POD` | Delete a pod by name. |
| `kubectl get pods -l app=APP` | List pods matching a label selector. |

## Deployments

| Command | Description |
| --- | --- |
| `kubectl get deployments` | List deployments in the current namespace. |
| `kubectl describe deployment DEPLOYMENT` | Show deployment configuration and events. |
| `kubectl create deployment NAME --image=IMAGE` | Create a deployment from an image. |
| `kubectl set image deployment/NAME CONTAINER=IMAGE` | Update a deployment container image. |
| `kubectl edit deployment DEPLOYMENT` | Edit a deployment manifest in the default editor. |
| `kubectl delete deployment DEPLOYMENT` | Delete a deployment and its managed resources. |
| `kubectl get rs` | List ReplicaSets in the current namespace. |

## Services

| Command | Description |
| --- | --- |
| `kubectl get services` | List services in the current namespace. |
| `kubectl describe service SERVICE` | Show service ports, selectors, and endpoints. |
| `kubectl expose deployment NAME --port=80 --target-port=8080` | Create a service for a deployment. |
| `kubectl get endpoints SERVICE` | Show endpoint addresses selected by a service. |
| `kubectl port-forward service/SERVICE 8080:80` | Forward a local port to a service port. |
| `kubectl delete service SERVICE` | Delete a service by name. |

## ConfigMaps & Secrets

| Command | Description |
| --- | --- |
| `kubectl get configmaps` | List ConfigMaps in the current namespace. |
| `kubectl create configmap NAME --from-literal=KEY=VALUE` | Create a ConfigMap from a literal value. |
| `kubectl create configmap NAME --from-file=PATH` | Create a ConfigMap from a file. |
| `kubectl get secret SECRET -o yaml` | Output a Secret manifest with encoded data. |
| `kubectl create secret generic NAME --from-literal=KEY=VALUE` | Create a generic Secret from a literal value. |
| `kubectl create secret tls NAME --cert=CERT --key=KEY` | Create a TLS Secret from certificate files. |
| `kubectl delete configmap NAME` | Delete a ConfigMap by name. |

## Namespaces & Nodes

| Command | Description |
| --- | --- |
| `kubectl get namespaces` | List all namespaces. |
| `kubectl create namespace NAMESPACE` | Create a namespace. |
| `kubectl get pods -n NAMESPACE` | List pods in a specified namespace. |
| `kubectl delete namespace NAMESPACE` | Delete a namespace and its contents. |
| `kubectl get nodes` | List cluster nodes. |
| `kubectl describe node NODE` | Show node capacity, conditions, and pods. |
| `kubectl cordon NODE` | Mark a node unschedulable. |
| `kubectl drain NODE --ignore-daemonsets` | Evict eligible workloads from a node. |

## Logs, Exec & Debugging

| Command | Description |
| --- | --- |
| `kubectl logs POD` | Print logs from a pod's default container. |
| `kubectl logs POD -c CONTAINER` | Print logs from a named container. |
| `kubectl logs -f POD` | Stream logs from a pod. |
| `kubectl logs POD --previous` | Print logs from the previous container instance. |
| `kubectl exec -it POD -- sh` | Open an interactive shell in a pod. |
| `kubectl cp POD:/path/file ./file` | Copy a file from a pod to the local machine. |
| `kubectl debug POD -it --image=busybox` | Add an ephemeral debugging container to a pod. |

## Scaling, Rollouts & Apply

| Command | Description |
| --- | --- |
| `kubectl scale deployment NAME --replicas=3` | Set the replica count for a deployment. |
| `kubectl autoscale deployment NAME --min=2 --max=10 --cpu-percent=80` | Create a CPU-based horizontal pod autoscaler. |
| `kubectl rollout status deployment/NAME` | Wait for and report rollout status. |
| `kubectl rollout history deployment/NAME` | Show deployment rollout revisions. |
| `kubectl rollout undo deployment/NAME` | Roll back a deployment to its previous revision. |
| `kubectl apply -f manifest.yaml` | Create or update resources from a manifest. |
| `kubectl apply -k DIRECTORY` | Create or update resources using Kustomize. |
| `kubectl delete -f manifest.yaml` | Delete resources defined in a manifest. |

## RBAC

| Command | Description |
| --- | --- |
| `kubectl get serviceaccounts` | List service accounts in the current namespace. |
| `kubectl get roles,rolebindings` | List namespace-scoped RBAC resources. |
| `kubectl get clusterroles,clusterrolebindings` | List cluster-scoped RBAC resources. |
| `kubectl create rolebinding NAME --clusterrole=view --serviceaccount=NAMESPACE:SA` | Bind the view ClusterRole to a service account. |
| `kubectl auth can-i VERB RESOURCE` | Check whether the current identity is authorized. |
| `kubectl auth can-i create pods --as=USER` | Check a user's permission through impersonation. |
