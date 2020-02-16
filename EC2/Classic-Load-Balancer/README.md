# Classic Load Balancer

#### Create Security grop for Admin access

* Go to Security Group features in EC2 
* Click on create security group
* Security Group Name - Admin SSH Access
* Type: SSH, protocol: ssh, port-range: 22, source: anywhere, description: SSH Access SG


#### Create SG for Application

* Go to Security Group features in EC2 
* Click on create security group
* Security Group Name - java Application 
* Type: Custom, protocol: tcp, port-range: 4567, source: anywhere, description: Java Application SG

### Create EC2 instances

* Create 2 EC2 instances using the [ Java Application AMI ](https://github.com/konman01/AWS/tree/master/EC2/create-ami)
* Attach 2 security groups created (Admin SSH Access, java Application) to the instances


### Classic Load Balancer Setup

* Go to load balancer feature in EC2
* Create Load Balancer
* Select the Classic Load Balancer
* Load Balancer - elb-for-javaapp
* Select Default VPC

Load balancer Protocol | Load Balancer Port | Instance Protocol | Instance Port
---------------------- | ------------------ | ----------------- | -------------
HTTP | 80 | HTTP | 4567

Load Balancer Protocol: Protocol that loadbalancer enables.  

Load Balancer port: Port at which the load balancer will be listening.  

Instancer Protocol: Protocol the instance uses. 

Instance Port: Port at which the instance will be listening. 

### Configure Security Group for the Load Balancer

* Click on create security group. 
* Security Group Name - Classic Load Balancer SG. 
* Type: Custom, protocol: tcp, port-range: 80, source: anywhere, description: Java Application SG. 

### Configure Health Check
ping protocol: HTTP (Protocol that the load balancer uses to ping the instancer). 

Ping port: 4567 (Port at which the instances will be listening). 

Response Time: 5 (Time with in which the load balancer expects the response from the server). 

Interval: 30 (Perform Health Check for every 30 secs). 

Unhealth Thresold: 2 (If the health check is wrong for 2 times in row, then instance is considered as unhealth). 

Unhealth Thresold: 5 (If the health check is right for 5 times in row, then instance is considered as health). 


### Add Instances

Add the two instances created to the load balancer. 

Review and Create

### Access the application through the browser

http://`<ip address of the laad balancer>`:80


### Add Security Group 

To enable the load balancers only to have access to the instances, then attach the load balancer SG created to the Java application SG as the inbound rule and delete the inbound rules of 4567 port. Then the instances attached to the load balancer will not be accessible by others. 

#### Delete the load balancer

#### Stop the instances