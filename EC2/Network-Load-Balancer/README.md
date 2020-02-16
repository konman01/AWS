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

### Create Load Balancer

* Create load balancer
* Network Load balancer
* Name: nlb-java-app
* Internet facing
* Listener: TCP Protocol, Port 80
* VPC: Default VPC


### Create Target Group


* Target group name: app-target-1
* Target Type: Instance
* Protocol: TCP
* Port: 4567

#### Health Check

* Protocol: TCP
* Port: Traffic Port (Traffic Port Mentioned above)
* Healthy Thresold: 5
* Unhealthy Thresold: 3
* Time out: 5 secs
* Interval: 10 secs


### Register target

#### Add the instance to the target group

* Go to target tab in app-target-1 target group
* Edit
* Add all the instances created using AMI and save

#### review and Create

### open application in Browser

http://`<elastic load balancer>`:80

	


