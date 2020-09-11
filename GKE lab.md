##LAB: Google Cloud Fundamentals: Getting Started with GKE


##Objectives: In this lab, you learn how to perform the following tasks:

	-Provision a Kubernetes cluster using Kubernetes Engine.

	-Deploy and manage Docker containers using kubectl.

##Steps:

1. Confirm that needed APIs are enabled by updating cloud SDK components.

	gcloud components update


2. Start a Kubernetes Engine cluster.

	export MY_ZONE=us-central1-a
	##This command variable "MY_ZONE" to represent the "us-central1-a" GCP region for convenience

	gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2
	##This command creates a cluster with two nodes, called "webfrontend" in the MY_ZONE region 

	kubectl version
	##To check the installed version of kubernetes


3. Run and deploy a container

	-Launch a single instance of the nginx container.

		kubectl create deploy nginx --image=nginx:1.17.10

	-View the pod running the nginx container:

		kubectl get pods

	-Expose the nginx container to the Internet:

		kubectl expose deployment nginx --port 80 --type LoadBalancer

	-View the new service:

		kubectl get services

			Result: The external IP is displayed. You can use the displayed external IP address to test and contact the nginx container remotely.

	-Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.

	-Scale up the number of pods running on your service:

		kubectl scale deployment nginx --replicas 3

	-Confirm that Kubernetes has updated the number of pods:

		kubectl get pods

	-Confirm that your external IP address has not changed:

		kubectl get services

	-Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.