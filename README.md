# prometheus-operator (安專教學)

## 步驟一: (下載CoreOS團隊開發的套件包)
    git clone https://github.com/coreos/kube-prometheus.git 
## 步驟二: (擴展**CustomResourceDefinition**)
### 資料夾位置
kube-prometheus ⇨ manifests ⇨ setup 
### 執行指令
    kubectl apply -f .
    
備註: 如有看到long: must have at most 262144 bytes 字樣的Error，請改用

    kubectl create -f X.yaml 建置
## 步驟三: (調整Yaml)
### 資料夾位置
kube-prometheus ⇨ manifests
### 執行項目 (新增NodePort參數)
* grafana-service.yaml
* prometheus-service.yaml
* alertmanager-service.yaml

例:
![image](https://github.com/Jerrychanglab/prometheus-operator/assets/39659664/aff386df-cd4a-472e-8f75-cc7d16884149)  
## 步驟四: (prometheus-operator部署)
### 資料夾位置
kube-prometheus ⇨ manifests
### 執行項目 (部署)
    kubectl apply -f .

## 步驟五: (檢查)
    kubectl get pod -n monitoring
備註: 查看是否有以下幾個Pod是否狀態正常
alertmanager-main
blackbox-exporter
grafana
kube-state-metrics
node-exporter
prometheus-adapter
prometheus-k8s
prometheus-operator
## 步驟六: (查看SVC連線端口)
    kubectl get svc -n monitoring
prometheus-k8s 9090:(NodePort)
grafana 3000:(NodePort)
alertmanager-main 9093:(NodePort)
