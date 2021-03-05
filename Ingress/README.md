Ingress
=======

Ingress is the application load balancer in the Kubernetes. Ingress is used to manage the external access to the services in a cluster.

How to use this code?
=====================

Step 1: Build the docker images
-------------------------------

Build the docker images using Dockerfiles in the services/ folder.

`$ docker build -t cankush625/mailapp:v1 ./services/mail/.`

`$ docker build -t cankush625/searchapp:v1 ./services/search/.`

Step 2: Create deployment for mail and search
---------------------------------------------

`$ kubectl create deployment mail --image=cankush625/mailapp:v1`

`$ kubectl create deployment search --image=cankush625/searchapp:v1`

Step 3: Expose mail and search deployments
------------------------------------------

`$ kubectl expose deploy mail --port=80 --type=NodePort`

`$ kubectl expose deploy search --port=80 --type=NodePort`

Step 4: make the entry in the local host file
---------------------------------------------

We always provide host name or domain name to the Ingress Controller. So, either we required the real domain name or we can create a local entry for domain name/host name in the local host file.

In linux, the host file is located at `/etc/hosts` and in windows, the host file is located at `C:\Windows\System32\drivers\etc\hosts`.<br>
In this demo, I will use www.example.com as a domain name(host name). And as I'm running the k8s cluster using minikube, the minikube is running on IP 192.168.99.100.

So, go to the host files mentioned above and add the following line.

`192.168.99.100     www.example.com`

Step 5: Create Ingress rule
---------------------------

For creating the Ingress rule, run one of the above configuration file depending on your kuberntes version.

`$ kubectl create -f ingress_resource.yml`

Step 6: Access the services
---------------------------

Now, we can access the mail and search services using the path we had added in the ingress rule.

`$ curl www.example.com:80/mail`

`$ curl www.example.com:80/search`