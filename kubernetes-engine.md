### LAB: Google Cloud Fundamentals: Getting started with Google Kubernetes Engine .(GKE)
## Objectives:
In this lab, we learn how to perform the following tasks;
Provision a Kubernetes cluster using Kubernetes Engine.
Deploy and manage Docker containers using kubectl.

Steps:
* Confirm that needed API’s are enabled 
-Enter the following to display the project IDs for your Google Cloud projects:
	```gcloud projects list```

-Using the applicable project ID from the previous step, set the default project to the one in which you want to enable the API:
	```gcloud config set project
YOUR_PROJECT_ID```

-Get a list of services that you can enable in your project:
	```gcloud services list --available```

If you don't see the API listed, that means you haven't been granted access to enable the API.

* Using the applicable service name from the previous step, enable the service:
```	gcloud services enable
SERVICE_NAME

* Start a Kubernetes Engine cluster.
	``Export MY_ZONE``
followed by the zone . Your complete command will look similar to this:
	``Export MY_ZONE=us-central1-a```

-Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster webfrontend and configure it to run 2 nodes:

	```gcloud container clusters create webfrontend  --zone$MY_ZONE --num-nodes2```
  
It takes several minutes to create a cluster as Kubernetes Engine provisions virtual machines for you.
-After the cluster is created, check your installed version of Kubernetes using the kubectl version command:
```Kubectl version```

The cloud container cluster command automatically authenticated kubectl for you.
Run and Deploy a container.
	-Launch a single instance of Nginx container( Nginx is a popular web server)
		```Kubectl create deploy nginx --image=nginx:1.17.10```
    
In Kubernetes, all containers run in pods. This use of the kubectl create command caused Kubernetes to create a deployment consisting of a single pod containing the nginx container. A Kubernetes deployment keeps a given number of pods up and running even in the event of failures among the nodes on which they run. In this command, you launched the default number of pods, which is 1.
If you see any deprecation warning about future version you can simply ignore it for now and can proceed further.
	-View the pod running the nginx container:
		```Kubectl get pods```
    
	-Expose the nginx container to the Internet:
		```Kubectl expose deployment nginx  --port 80  --typeLoadBalancer```
    
	Kubernetes created a service and an external load balancer with a public IP address attached to it. The IP address remains the same for the life of the service. Any network traffic to that public IP address is routed to pods behind the service: in this case, the nginx pod.
	-View the new service:
		```Kubectl get services```
    
You can use the displayed external IP address to test and contact the nginx container remotely.
It may take a few seconds before the External-IP field is populated for your service. This is normal. Just re-run the kubectl get services command every few seconds until the field is populated.
-Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
-Scale up the number of pods running on your service:
```Kubectl scale deployment nginx --replicas 3```

Scaling up a deployment is useful when you want to increase available resources for an application that is becoming more popular.
-Confirm that Kubernetes has updated the number of pods:
	```Kubectl get pods```
  
-Confirm that your external IP address has not changed:
   ```Kubectl get services```
-Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.
 
 
 

	

	


