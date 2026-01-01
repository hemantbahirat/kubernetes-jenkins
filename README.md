# Kubernetes Manifests for Jenkins Deployment

Refer https://devopscube.com/setup-jenkins-on-kubernetes-cluster/ for step by step process to use these manifests.

# Jenkins link
http://192.168.65.3:32000/

# If PVC is full and storageclass supports expansion:

kubectl -n devops patch pvc jenkins-pv-volume -p '{"spec":{"resources":{"requests":{"storage":"30Gi"}}}}'
Then follow your storage provider docs to expand the PV filesystem (or run kubectl rollout restart deploy <jenkins-deploy> after expansion if dynamic resizing supported).


kubectl create namespace devops
kubectl apply -f serviceAccount.yaml
kubectl get nodes
kubectl create -f volume.yaml
kubectl apply -f deployment.yaml
kubectl get deployments -n devops
kubectl describe deployments --namespace=devops
kubectl apply -f service.yaml

http://<node-ip>:32000

kubectl get pods --namespace=devops
kubectl logs jenkins-deployment-2539456353-j00w5 --namespace=devops
OR
kubectl exec -it jenkins-559d8cd85c-cfcgk cat /var/jenkins_home/secrets/initialAdminPassword -n devops
