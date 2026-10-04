# K8s 101

Examples for the **K8s 101** series on [rivaldito.com](https://rivaldito.com). Each folder matches a topic of the series.

## Requirements

- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [minikube](https://minikube.sigs.k8s.io/docs/start/)

```bash
minikube start
```

## Pods

Post (in Spanish): [K8s 101, el manifiesto como estilo de vida #3](https://rivaldito.com/es/software/k8s-101-el-manifiesto-3)

| File | What it shows |
| --- | --- |
| `Pods/pod.yaml` | Our first manifest, a Pod with a single nginx container |
| `Pods/multiplesPods.yaml` | Two Pods in a single file, separated by `---` |
| `Pods/podTwoContainers.yaml` | A Pod with two containers fighting over the same port (ends in `CrashLoopBackOff`, on purpose) |
| `Pods/labels.yaml` | Two Pods with `app` and `env` labels |

### Usage

```bash
# create
kubectl apply -f Pods/pod.yaml

# inspect
kubectl get pods
kubectl describe pod nginx
kubectl logs nginx

# delete
kubectl delete -f Pods/pod.yaml
```

For the two-container example, read each container's logs with `-c`:

```bash
kubectl apply -f Pods/podTwoContainers.yaml
kubectl logs pythonservers -c pythonservertwo
```

To filter by labels:

```bash
kubectl apply -f Pods/labels.yaml
kubectl get pods -l app=frontend
kubectl get pods --show-labels
```

When you are done, clean up with `kubectl delete -f` on the same file.
