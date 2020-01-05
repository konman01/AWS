	

     
###Select EC2 Service in AWS Management Console

### Launch Instance
1. Select Oregon Availability Zone
2. Click on Launch Instance Button
3. Amazon Linux AMI: Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type
4. Instance Type: t2.micro 

### Configure Instance Details
Number of Instances: 1

Network: Default

Subnet: No preference

Auto Assign Public IP: Enable

Shutdown Behaviour: Stop

Go to Advance Details

Select the text type

Paste the following commands. All the below command will be executed in Admin access by default 
  
  \#!/bin/bash
  
  yum update -y
  
  yum install -y httpd
  
  service httpd start
  
  chkconfig httpd on


### Add Storage
Keep the default EBS (Elastic Block Storate) allocated by AWS to EC2 instance

### Add Tad
Key: Name
Value: Amazon Linux

### Security Group
Select existing Secutity Group : my-first-instance

#### Add http port along with ssh in my-first-instance SG

Type: http, protocol: tcp, port-range: 80, source: anywhere, description: http enabled

Click review and launch

### Select a key pair


### Connect to AWS from system terminal

	ssh -i ec2-masterclass.pem ec2-user@<public-ip-address>


### Stop or Terminate the instance







