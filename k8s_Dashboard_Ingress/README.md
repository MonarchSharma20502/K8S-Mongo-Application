FIRST WE NEED TO INSTALL INGRESS CONTROLLER IN THE KUBERNETES CLUSTER.
AS WE ARE USING MINIKUBE, WE CAN INSTALL THE INGRESS CONTROLLER USING THE FOLLOWING COMMAND:
COMMAND - 'minikube addons enable ingress' 


IF WE WERE WORKING ON KUBERNETES, WE WOULD HAVE RUN THE FOLLOWING COMMAND:
COMMAND - 'kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.0/deploy/static/provider/cloud/deploy.yaml'

Here are all the resources available in the kubernetes-dashboard namespace:
![kubectl get all -n kubernetes-dashboard](Resources%20in%20dashboard%20namespace.png)

We now apply the Ingress configuration file to create the routing rules for the ingress controller using,
COMMAND - 'kubectl apply -f dashboard-ingress.yaml'
Now we have added and deployed the ingress component and we can see the deployed ingress resource getting private IP address
![ingress-deployment](Ingress%20Resource.png)

We must perform Host File Entry in the /etc/hosts (linux OS) or C:\Windows\System32\drivers\etc\hosts (windows OS) for the IP and the domain provided in the Ingress configuration (dashboard.com) so that we can resolve the IP address (e.g., 192.169.64.5) to the domain name and can access the dashboard.
RESULT - Now we can see that the ingress is configured.