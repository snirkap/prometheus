# prometheus
commands:
kind create cluster --name=snir
helm repo add prometheus-community https://prometheuscommunity.github.io/helm-charts
helm repo update
kubectl create namespace monitoring
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz 
tar -zxvf ngrok-v3-stable-linux-amd64.tgz 
./ngrok config add-authtoken 2QCcclEE80tINnI1Gx8QMyKLFbr_4hscbjiAdumc5BjHBiNwN
kubectl port-forward service/prometheus-kube-prometheus-prometheus -n monitoring 9090:9090 --address='0.0.0.0' &
./ngrok http 0.0.0.0:9090

