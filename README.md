curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-172.0.1-linux-x86_64.tar.gz
tar -zxvf google-cloud-sdk-172.0.1-linux-x86_64.gz
rm google-cloud-sdk-172.0.1-linux-x86_64.tar.gz
./google-cloud-sdk/install.sh

gcloud init


gcloud components install kubectl

gcloud container clusters create demo-cluster

kubectl apply -f --recursive=true apps/

kubectl expose rc nginx --port=80
kubectl expose rc aggregator --port=8080

kubectl proxy --www=${PWD}/www/

kubectl scale rc nginx --replicas=10
kubectl scale rc vegeta --replicas=10

kubectl rolling-update nginx --image=gcr.io/google_containers/nginx-scale:0.3
