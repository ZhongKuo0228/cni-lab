# 在 eks 安裝 calico

安裝 cluster

```jsx
eksctl create cluster --name my-calico-cluster --without-nodegroup
```

刪除 daemon 

```jsx
kubectl delete daemonset -n kube-system aws-node
```

---

operator

install operator

```jsx
kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.3/manifests/tigera-operator.yaml
```

install calico configure

`calico.yml`

```jsx
kind: Installation
apiVersion: operator.tigera.io/v1
metadata:
  name: default
spec:
  kubernetesProvider: EKS
  cni:
    type: Calico
  calicoNetwork:
    bgp: Disabled
```

```jsx
eksctl create nodegroup --cluster my-calico-cluster --node-type t3.medium --max-pods-per-node 100
```

---

manifest

安裝 calico manifest

```jsx
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.3/manifests/calico-vxlan.yaml
```

disable aws src/dst checks

```jsx
kubectl -n kube-system set env daemonset/calico-node FELIX_AWSSRCDSTCHECK=Disable
```

add nodes

```jsx
eksctl create nodegroup --cluster my-calico-cluster --node-type t3.medium --max-pods-per-node 100
```

ref

https://docs.tigera.io/calico/latest/getting-started/kubernetes/managed-public-cloud/eks

---

查看

```jsx
kubectl get pods -n calico-system
```

確認 node cni