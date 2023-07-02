# prometheus
commands:
kind create cluster --name=snir
helm repo add prometheus-community https://prometheuscommunity.github.io/helm-charts
helm repo update
kubectl create namespace monitoring
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz 
tar -zxvf ngrok-v3-stable-linux-amd64.tgz 
./ngrok config add-authtoken 2S14mCUm5dQYtdSrSW2ngDhEyu5_29XbaRq3cPCbqSBLaCKVe 

