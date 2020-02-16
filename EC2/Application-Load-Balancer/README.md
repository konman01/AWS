# Application Load Balancer

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


### Create Target Group 1


* Target group name: app-target-1
* Target Type: Instance
* Protocol: HTTP
* Port: 4567
* VPC: Default

#### Health Check

* Protocol: HTTP
* Path: /health
* Port: Traffic Port (Traffic Port Mentioned above)
* Healthy Thresold: 5
* Unhealthy Thresold: 2
* Time out: 5 secs
* Interval: 10 secs
* Sucess Code: 200

#### Add the instance to the target group

* Go to target tab in app-target-1 target group
* Edit
* Add 1st instance created using AMI and save


### Create Target Group 2


* Target group name: app-target-2
* Target Type: Instance
* Protocol: HTTP
* Port: 4567
* VPC: Default

#### Health Check

* Protocol: HTTP
* Path: /health
* Port: Traffic Port (Traffic Port Mentioned above)
* Healthy Thresold: 5
* Unhealthy Thresold: 2
* Time out: 5 secs
* Interval: 10 secs
* Sucess Code: 200

#### Add the instance to the target group

* Go to target tab in app-target-2 target group
* Edit
* Add 2nd instance created using AMI and save


### Create Load Balancer

* Create load balancer
* Application Load balancer
* Name: alb-java-app
* Internet facing
* Listener: HTTP Protocol, Port 80
* VPC: Default VPC

### Configure Security Group for the Load Balancer

* Click on create security group. 
* Security Group Name - Application Load Balancer SG. 
* Type: Custom, protocol: tcp, port-range: 80, source: anywhere, description: Application Load Balancer

### Select Target Group

* Target Group: app-target-1
* target type: instance
* All other values will be updated by default as we set in the target group

#### Register target

#### Review and Create

### Add the routes

* Select Listener of the Application Load Balancer
* View and edit the rules
* Add the following Conditions
![image](https://github.com/konman01/AWS/blob/master/images/conditions.png)

### Access the application through the browser

http://`<ALB URL>`/ -> will be directed to target group 1. 


http://`<ALB URL>`/details -> will be directed to target group 2. 


### Add Security Group 

To enable the load balancers only to have access to the instances, then attach the Application load balancer SG created to the Java application SG as the inbound rule and delete the inbound rules of 4567 port. Then the instances attached to the load balancer will not be accessible by others. 


#### Delete the load balancer

#### Stop the instances


