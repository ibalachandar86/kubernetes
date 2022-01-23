# Run test.yaml
vi /home/ibalachandar86/yamls/test.yaml
kubectl create -f /home/ibalachandar86/yamls/test.yaml
kubectl delete pod {podname}
kubectl get pods

# Run memory.yaml
kubectl create namespace mem-example
alias k8="kubectl -n mem-example"
vi /home/ibalachandar86/yamls/memory.yaml
k8 create -f /home/ibalachandar86/yamls/memory.yaml
k8 delete pod {podname}
k8 get pods
k8 exec -it memory-demo -- /bin/bash
stress --vm 1 --vm-bytes 150M --vm-hang 1

# Run deployment.yaml
kubectl create namespace test
alias k8="kubectl -n test"
vi /home/ibalachandar86/yamls/deployment.yaml
k8 delete deployment nginx-deployment
k8 create -f /home/ibalachandar86/yamls/deployment.yaml
k8 get deployments
k8 rollout status deployment/nginx-deployment
k8 get pods
k8 exec -it memory-demo -- /bin/bash
