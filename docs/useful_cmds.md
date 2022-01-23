# Useful Commands
sudo -i
kubectl get nodes
kubectl describe nodes
kubectl get pods
watch kubectl get pods
kubectl get pods -w
kubectl get sts
kubectl get nodes -o wide
kubectl get pods -n kube-system
kubectl get pods -A -o wide
ps -ef | grep api-server
kubectl get pods -A -o wide | grep -i coredns
ls -l /etc/kubernetes/manifests
cat ~/.kube/config
kubectl api-resources
vi ~/.bashrc
alias k8 = kubectl
kubectl run nginx --image=nginx --dry-run=client
kubectl run tomcat --image=tomcat --dry-run=client
kubectl create -f *.yaml
kubectl create -f *.yaml -n {namespacename}
kubectl create -f /home/ibalachandar86/yamls/test.yaml
kubectl delete -f *.yaml
kubectl get pod -o yaml
kubectl get pod -o yaml > another.yaml
kubectl get ns
kubectl create ns {namespacename}
kubectl describe pod {podname}
kubectl exec -it {podname} -- bash
kubectl logs pod {podname}
kubectl get pods --selector environment=production
kubectl get pods -A | grep -i scheduler
kubectl describe node
kubectl get rs #ReplicaSet
k scale --replicas=4 rs {Replica set name}