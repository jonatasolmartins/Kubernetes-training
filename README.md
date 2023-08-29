# KUBERNETES
 This a repository I created to save the important command I've leran during my Kubernetes trainning.

 ## Table of contents

- [Dashboard](#dashboard)
  - Deploy a the Kubernetes dashboard
- [Pods](#run-container)
  - Run your first pod
- [Deployment](#deployment)
  - Create a deployment for our pod
- [The Get Command](#get-command)
- [Bonus tricks](#bonus-commands)
  - Call a pod from another pod using curl
- [K3d commands](#k3d-commands)
  - Working with k3d Kubernetes



## Dashboard
To use Kubernete dashboard:

    kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
    kubectl apply -f dashboard-adminuser.yml  
    kubectl -n kubernetes-dashboard create token admin-user
    kubectl proxy
    http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
    kubectl -n kubernetes-dashboard delete serviceaccount admin-user
    kubectl -n kubernetes-dashboard delete clusterrolebinding admin-user

## Run Container
    kubectl run my-nginx --image=nginx:alpine  
    kubectl create -f nginx.pod.yml --dry-run=client --validate=true
    kubectl create -f nginx.pod.yml --save-config
    kubectl apply -f nginx.pod.yml
    kubectl port-forward pod/nginx-pod 8080:80
    kubectl port-forward deployment/node-app 8080:
    kubectl port-forward service/nginx-server 8080:80
    kubectl delete pod nginx-pod
    kubectl delete service my-nginx
    kubectl exec nginx-pod -c my-nginx -i -t -- sh
  
## Deployment
  Use this:

    kubectl create -f nginx.deployment.yml --save-config

  Or use this:

    kubectl apply -f nginx.deployment.yml
  
  Scale the deployment pods
  
    kubectl scale deployment my-deployment-name --replicas=5

  Or 

    kubectl scale -f nginx.deployment.yml --replicas=5

  ### Delete a deployment

    kubectl delete -f nginx.deployment.yml
  
    
## Get Command
    > kubectl get all
    > kubectl get pods
    > kubectl get deployments
    > kubectl get deployments --show-labels
    > kubectl get deployment -l app=my-label-name
    > kubectl get services
    > kubectl describe nginx-pod

## Bonus Commands
 Enter the pod on interactive mode:

     > kubectl exec nginx-pod -c my-nginx -i -t -- sh
 on alpine, add curl if it's not present:

     > apk add curl

 Get the PodIp or ServiceIp using the Kubectl get command

     > Kubectl get pods
     > Kubectl get services

 Them call the desired pod using it podIP, the serviceIp of the pod or the service name(this is the DNS name of the service)

     > curl -s http://10.99.22.129
     > curl -s http://nginx-cluster:80

## K3d Commands

  #### Get version and info
     k3d info
     k3d version
     
  #### Start the cluster
     k3d cluster start dev-cluster
    
  #### Import local images to the cluster
     k3d image import node-app:1.0 -c dev-cluster