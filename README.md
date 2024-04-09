# K8s 網路模型與 CNI

## 本次討論題目

實際搭建以下幾種 CNI 並和 AWS CNI 進行原理、優缺點和效能的比較

https://github.com/flannel-io/flannel
https://github.com/projectcalico/calico
https://github.com/weaveworks/weave/
https://github.com/cilium/cilium


## 說明簡報

本次分享會先說明 K8s 的網路基本原則，並說明 CNI 能夠協助 K8s 如何管理 Pod 的網路資源與對應的使用情境，後續提供 Lab 步驟與數據佐證各項 CNI 工具的效能。

https://docs.google.com/presentation/d/12KyduZQJ3sM1Vu3n6hiw0RXc8zF2ESasQkBHgLcGYlw/edit#slide=id.p

[簡報 PDF](./K8s%20網路模型與%20CNI.pdf)

## Lab 說明

### 在 EKS 上安裝第三方 CNI 的方式

本次提供 calico 與 calico 在 EKS 上的安裝方式

- [在 eks 安裝 calico](./在%20eks%20安裝%20calico.md)
- [在 eks 安裝 cilium](./在%20eks%20安裝%20cilium.md)

### 使用 Minikube 測試 CNI 效能的方式

說明如何透過 Minikube 測試 CNI 效能的方式，主要觀察

1. CNI 對於 Pod 建立時間是否有影響
2. `同 WorkerNode`與`跨 WorkerNode` 間傳輸效率
3. CNI 使用運算資源的狀態

[Lab 說明文件](./K8s%20網路模型與%20CNI.pdf)以 Flunnel 爲例，可以自行更換 [MiniKube 的 CNI Plug-in](https://minikube.sigs.k8s.io/docs/commands/start/) 進行比較


### 使用 Minikube 錄製 CNI 網路封包的方式

說明如何[在 Minikube 錄製 CNI 網路封包](./錄%20CNI%20的網路封包.md)，以驗證 CNI 網絡封包的傳遞過程
