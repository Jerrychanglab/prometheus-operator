# prometheus-operator (安專教學)

## 步驟一: (下載CoreOS團隊開發的套件包)
    git clone https://github.com/coreos/kube-prometheus.git 
## 步驟二: (擴展**CustomResourceDefinition**)
kube-prometheus ⇨ manifests ⇨ setup
執行指令:
    kubectl apply -f .
如有看到long: must have at most 262144 bytes 字樣的Error，請改用
    kubectl create -f X.yaml 建置
## 步驟三: (部署prometheus-operator)
請先調整三隻Yaml，新增Type: NodePort
grafana-service.yaml
prometheus-service.yaml
alertmanager-service.yaml

kube-prometheus ⇨ manifests
kubectl apply -f .
