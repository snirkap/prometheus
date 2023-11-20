# monitor project 
This project aims to provide a comprehensive monitoring solution using Prometheus and Grafana. It includes the integration of Redis with a Grafana plugin, there is also a  connection to Prometheus RabbitMQ through ServiceMonitor with Prometheus operator. Additionally, a dashboard for RabbitMQ has been created using a custom ConfigMap.
and you have a dashbord for your node that called "Node Exporter / Nodes".
## Setup:
1. minikube start --driver=docker 
2. git clone https://github.com/snirkap/prometheus.git 
3. cd prometheus/ 
4. kubectl create namespace monitoring 
5. kubectl create namespace redis 
6. kubectl create namespace rabbitmq 
7. helm repo add prometheus-community https://prometheuscommunity.github.io/helm-charts 
8. helm repo add bitnami https://charts.bitnami.com/bitnami 
9. helm repo update 
11. helm install prometheus prometheus-community/kube-prometheus-stack -f prometheus-values.yaml -n monitoring 
12. helm install my-redis bitnami/redis -f redis-values.yaml -n redis 
13. helm install my-rabbitmq bitnami/rabbitmq -f rabbitmq-values.yaml -n rabbitmq 
14. kubectl apply -f configmap.yaml -n monitoring 
15. kubectl port-forward service/prometheus-kube-prometheus-prometheus -n monitoring 9090:9090 --address='0.0.0.0' & 
16. kubectl port-forward service/prometheus-grafana -n monitoring 8080:80 --address='0.0.0.0' &
## tutorial:
### this is the files i used to configure the defult chart of Prometheus, Redis, and RabbitMQ.
* prometheus-values.yaml
  ```
  grafana:
  enabled: true
  plugins:
    - redis-datasource
    - redis-app
  apps:
    - type: redis-app
      disabled: false
  additionalDataSources:
    - name: redis
      type: redis-datasource
      access: proxy
      editable: true
      orgId: 1
      url: redis://my-redis-master.redis:6379
      jsonData:
        client: standalone
        poolSize: 5
        timeout: 10
        pingInterval: 0
        pipelineWindow: 0
      secureJsonData:
        password: 123
      version: 1
  ...
  ruleSelectorNilUsesHelmValues: false
  ...
  serviceMonitorSelectorNilUsesHelmValues: false
the first change is to add "redis-datasource" and "redis-app" plugins to grafana and after that create a new datasource in grafana for reids (for access redis grafana will need a password). The next two changes enable Prometheus to access rules and ServiceMonitors beyond the default Helm values. By setting 'ruleSelectorNilUsesHelmValues' and 'serviceMonitorSelectorNilUsesHelmValues' to false, Prometheus is configured to use the actual cluster resources for rules and ServiceMonitors rather than relying only on the Helm values. This modification provides flexibility in selecting and monitoring resources within the cluster.

* redis-values.yaml
  ```
  auth:
    password: "123"
  metrics:
    enabled: true
    serviceMonitor:
      enabled: true
      additionalLabels:
        app.kubernetes.io/component: metrics
    prometheusRule:
      enabled: true
      namespace: "redis"
The first two lines define a password to redis for grafana to be able to connect direct to redis as data-source, the next changes enable the scraping of metrics from a Redis service and create a ServiceMonitor specifically for the Redis metrics-gathering service identified by the label app.kubernetes.io/component: metrics. Additionally, it enables the Prometheus rules in the redis namespace.

* rabbitmq-values.yaml
  ```
  metrics:
  enabled: true
  podAnnotations:
    prometheus.io/path: /metrics
    prometheus.io/scrape: "true"
    prometheus.io/port: "9419"
  serviceMonitor:
    enabled: true
    labels:
      release: prometheus
    selector:
      app.kubernetes.io/instance: my-rabbitmq
    namespace: rabbitmq
    path: /metrics
    interval: 30s
    scrapeTimeout: 15s
  prometheusRule:
    enabled: true
    namespace: rabbitmq
These changes enable the scraping of RabbitMQ pod metrics with Prometheus. It establishes pod annotations, creates a ServiceMonitor with specific configurations that also contain "release: prometheus" lable that allows prometheus to follow the servicemonitor and collect from him metrics from rabbitmq, and activates Prometheus rules in the designated namespace. These changes support the collection and monitoring of RabbitMQ metrics.
* configmap.yaml
  ```
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: clusterinfo
    labels:
      grafana_dashboard: "1"
  data:
    dashboard1.json: |-
    {
      ...
      ...
      ...
    }
This sidecar looks for ConfigMap in the same namespace as the Grafana pod , with the label “grafana_dashboard” set to “1”.
and inside the "dashboard1.json:" i put the full json file of the rabbitmq dashbord. 
It is important to note that this dashboard was created using the 'RabbitMQ-Overview' dashboard available in the Grafana store. The dashboard can be found at the following link: https://grafana.com/grafana/dashboards/10991-rabbitmq-overview/. The entire content and design of the dashboard are based on the pre-existing 'RabbitMQ-Overview' dashboard available in the Grafana store.

  


