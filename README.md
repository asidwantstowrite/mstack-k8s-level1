# mstack-k8s-level1
1) create a service account with admin privileges and save the json credentials of that project

2) set the variable on the local system
export GOOGLE_APPLICATION_CREDENTIALS="/home/arshad/Desktop/mstack/mstack-level-1-801cd207f79d.json"

3) set the region and zone of gcp
gcloud config set compute/region asia-south1
gcloud config set compute/zone asia-south1-a

4) create the k8s cluster named mstack-l1 with 3 nodes using preemtible nodes to save some bucks
gcloud container clusters create mstack-l1 --num-nodes=3 --preemptible

5) get the k8s cluster config on your local system
gcloud container clusters get-credentials mstack-l1 --zone=asia-south1-a

# For staging environment
1) Goto staging-guestbook folder and run below commands sequentially

kubectl apply -f staging-ns.yaml
kubectl apply -f redis-master-deployment.yaml -f redis-master-service.yaml
kubectl apply -f redis-slave-deployment.yaml -f redis-slave-service.yaml
kubectl apply -f guestbook-deployment.yaml -f guestbook-service.yaml

# For production environment
1) Goto production-guestbook folder and run below commands sequentially

kubectl apply -f staging-ns.yaml
kubectl apply -f redis-master-deployment.yaml -f redis-master-service.yaml
kubectl apply -f redis-slave-deployment.yaml -f redis-slave-service.yaml
kubectl apply -f guestbook-deployment.yaml -f guestbook-service.yaml

# Creating ingress controller and ingess rules
1) Goto ingress-nginx-controller folder and run below commands for sequentially

kubectl apply -f mandatory.yaml
kubectl apply -f nginx-ingress-service.yaml
kubectl apply -f default-backend.yaml
kubectl apply -f ingress-rules-staging.yaml
kubectl apply -f ingress-rules-production.yaml

