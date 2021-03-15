# kubernetes
git clone https://github.com/seelammanoj/kubernetes.git

git checkout hello-kubernetes

Steps to setup the deployment of an application and creating service

using ingress-nginx to route the traffic from externally to the kubernetes cluster

app name: hello-kubernetes

container port is at: 8080

service port is at: 8000

attached Ingress resource yaml file: sample-ingress.yaml

Note: Before using the ingress-nginx controller, we should disable the traefik ingress controller

-> To disable the traefik, make the below changes in the k3s.service

        ExecStart=/usr/local/bin/k3s \
        server \
        --disable traefik \

-> Now, restart the k3s.service 

        sudo systemctl daemon-reload 
        sudo systemctl restart k3s.service 

-> Check the traefik ingress controller is running or not 

       kubectl get deployments -n kube-system
       
This should show no traefik running

-> Then enable the ingress-nginx controller, by the following the below link

        https://dev.to/sr229/how-to-use-nginx-ingress-controller-in-k3s-2ck2

Now, steps to deploy hello-kubernetes app and service

        1. kubectl apply -f sample-hello.yaml 
Check the deployments and service are created, by the below command

        2. kubectl get pods -o wide
        3. kubectl get deployment -o wide
        4. kubectl get service -o wide 
       
All the above commands should lists the pods, service, deployment for hello-kubernetes app

Now, apply the ingress resource to route the external traffic to the cluster via service

        5. kubectl apply -f sample-ingress.yaml 
       
After running the above command, you should able to see ingress resource created for the hello-kubernetes
Check, the ingress resource by the below command 

        6. kubectl get ingress -o wide

All done!!!

Now, Try to access the hello-kubernetes application from machine where kubernetes cluster is running or from outside cluster network 

To check using curl 

        7. curl http://<IP of the physical machine/VM where cluster is running> 

To check using browser 

Open your browser and type the below url in the search box 

        http://<IP of the physical machine/VM where cluster is running>
