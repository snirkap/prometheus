# prometheus
## enter google cloud shell and do this commands:
### commands:
1. kind create cluster --name=snir
2. helm repo add prometheus-community https://prometheuscommunity.github.io/helm-charts
3. helm repo update
4. kubectl create namespace monitoring
5. helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring
6. wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz 
7. tar -zxvf ngrok-v3-stable-linux-amd64.tgz 
8. ./ngrok config add-authtoken 2QCcclEE80tINnI1Gx8QMyKLFbr_4hscbjiAdumc5BjHBiNwN
9. kubectl port-forward service/prometheus-kube-prometheus-prometheus -n monitoring 9090:9090 --address='0.0.0.0' &
10. ./ngrok http 0.0.0.0:9090

