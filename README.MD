# Cryostat Local Setup

## Local k8s kind

[Install k8s kind](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

```shell
# Create new cluster and configure kubectl
kind create cluster --config ./kind/config.yaml && kind export kubeconfig --kubeconfig $HOME/.kube/config
```

## Cryostat Operator

```shell
# clone repo holding the kustomization for installing the operator
git clone https://github.com/cryostatio/cryostat-operator.git
# prepare the empty cluster for the operator
kubectl apply -f prepare.yaml
# install operator by shipped kustomization
kubectl apply -k kubectl apply -k cryostat-operator/config/default/
```

## Cryostat

```shell
# instruct operator by creating the Cryostat resource
kubectl apply -f cryostat.yaml
```

## Access

```shell
# forward ClusterIP service to host network
kubectl port-forward -n cryostat-operator-system svc/cryostat 8181:8181
```

## Cleanup

```shell
# Destroy kind cluster
kind delete cluster
```
