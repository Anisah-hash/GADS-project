## LAB: Google cloud fundamentals : Getting started with compute Engines.

### Objectives: 
In this lab you will learn how to perform the following tasks;
Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) console.
Create a Compute Engine virtual machine using the gcloud command line interface.
Connect between the two instances.

Steps:
* Create a Compute Engine virtual machine using the Google Cloud Platform(GCP)
	```gcloud compute instance create my-vm-1 --machine-type “n1-standard-1” --image project “debian-gcloud” --image “debian-9-stretch-v20190213” --subnet “default” --tags http ```
```gcloud compute firewall-rules create allow-http --action=allow --destination: INGRESS --rules=http “at --target-tags=http```


I will explain what the commands do, I’m creating a my-vm-1 with the machine type n1-standard-1, using a debian image (OS of the vm) with the subnet “default” this is a network and network tags of “http” which will apply the firewall rules to the vm that have the hhtp tag.
Then I will be creating a firewall rule which allows the incoming traffic of an http protocol with the vm of tags of http.

* Create a Compute Engine virtual machine using the gcloud command line interface.
	```Gcloud config set compute/zone us-central1-b```
```gcloud compute instance create  “my-vm-2” --machine-type “n1-standard-1” --image-project “debian-gcloud” --image “debian-9-stretch-v20190213” --subnet “default” ```

* Connect between the two instances.
	-To open a command prompt on my-vm-2 instance.
		```gcloud compute ssh my-vm-2```

	-Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network.
		```Ping -c4  my-vm-1```

	-Use the ssh command to open a command prompt on my-vm-1:
		```Ssh my-vm-1```

	-Install the Nginx web server at the command prompt
		```Sudo-apt-get install nginx-light -y```

	-Use nano text editor to add a custom message to the home page of the web server.
		```Sudo nano  /var/ww/html/index.nginx-debian.html```


Use the arrow keys to move the cursor just below the h1 header add text like this and replace YOUR_NAME with your name:

* Hi from YOUR_NAME*

	-Close the nano text editor.

	* Confirm that the web server is serving your new page at the command prompt on my-vm-1 execute the following command*

		```Curl http ://localhost/```
		* The result will be the HTML source of the web server’s home page, including your line of custom text.*

	-To exit the command prompt on my-vm-1 execute:
		Exit
			
			* To confirm that my-vm-2 can reach the web server on my-vm-1 at the command prompt on my-vm-2, execute this command:*
				
				```Curl http ://my-vm-1/```
				* The result will be the HTML source of the web server’s home page,including your line of custom text.*

			* Copy the External IP address of my-vm-1 and paste it to the address bar of a new browser tab.*
				```Gcloud compute instances list --zone us-central1-a```

 You will see your web server’s home page, including your custom text.
									




	

	
	


