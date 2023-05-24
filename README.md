# prometheus-operator (Install Teaching)

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
* alertmanager-main : 接收來自Prometheus Server的告警，並進行處理。

* blackbox-exporter : 偵測網路服務目標功能(HTTP、DNS、TCP...)，並提供給Prometheus監控數據。

* grafana : 抽取Prometheus的數據，提供客製化繪圖呈現。

* kube-state-metrics : 

* node-exporter : 收集每個k8s Node上的CPU、記憶體、網路流量...使用率指標，提供給Prometheus監控數據。

* prometheus-adapter : 監控Pod的資源使用指標，提供給HPA(Autoscaler)使用。

* prometheus-k8s : 監聽Kubernetes API Server，根據配置的監控目標（如 Service、Pod、Node)定期抓取指標數據，並將其存儲在本地的時間序列數據庫中。

* prometheus-operator : 管理組件並根據，Prometheus Operator 的自定義資源定義（Custom Resource Definitions，CRDs）來創建和管理 Prometheus、Alertmanager、ServiceMonitor 等資源。

## 步驟六: (查看SVC連線端口)
    kubectl get svc -n monitoring
### 需確認以下三個NodePort端口
例:

![image](https://github.com/Jerrychanglab/prometheus-operator/assets/39659664/b5ef8645-6ff7-4fb1-9b29-2b8482c6390b)
* prometheus-k8s 
* grafana
* alertmanager-main
