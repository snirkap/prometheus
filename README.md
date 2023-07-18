# prometheus
## commands:
1. minikube start --driver=docker .
2. git clone https://github.com/snirkap/prometheus.git .
3. cd prometheus/ .
4. kubectl create namespace monitoring .
5. kubectl create namespace redis .
6. kubectl create namespace rabbitmq .
7. helm repo add prometheus-community https://prometheuscommunity.github.io/helm-charts .
8. helm repo add bitnami https://charts.bitnami.com/bitnami .
9. helm repo update .
11. helm install prometheus prometheus-community/kube-prometheus-stack -f prometheus-values.yaml -n monitoring .
12. helm install my-redis bitnami/redis -f redis-values.yaml -n redis .
13. helm install my-rabbitmq bitnami/rabbitmq -f rabbitmq-values.yaml -n rabbitmq .
14. 
15. kubectl port-forward service/prometheus-kube-prometheus-prometheus -n monitoring 9090:9090 --address='0.0.0.0' & .
16. kubectl port-forward service/prometheus-grafana -n monitoring 8080:80 --address='0.0.0.0' & .
### redis:
1. clone the deploy and service
2. kubectl apply -f redis-master-deployment.yaml -n monitoring
3. kubectl apply -f redis-master-service.yaml -n monitoring
4. helm install redis-exporter prometheus-community/prometheus-redis-exporter -f prometheus-redis_values.yaml -n monitoring
5. kubectl port-forward service/redis-exporter-prometheus-redis-exporter -n monitoring 9121:9121 --address='0.0.0.0' &  ### this command to check that the exporter is give a metric
