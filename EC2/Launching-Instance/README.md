# Launching Instance

Select EC2 Service in AWS Management Console

### Launch Instance
* Select Oregon Availability Zone
* Click on Launch Instance Button
* Amazon Linux AMI: Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type
* Instance Type: t2.micro 

### Configure Instance Details
* Number of Instances: 1
* Network: Default
* Subnet: No preference
* Auto Assign Public IP: Enable
* Shutdown Behaviour: Stop

### Add Storage
Keep the default EBS (Elastic Block Storate) allocated by AWS to EC2 instance

### Add Tad
Key: Name
Value: Amazon Linux

### Security Group
* Select New Secutity Group 
* Security Group Name: my-first-instance
* Description: My First Security Group Created for AMS Linux

Type: ssh, protocol: tcp, port-range: 22, source: anywhere, description: ssh is enables

* Click review and launch

### Create a key pair

* create a new key pair
* name: ec2-masterclass
* download the keypair
* Never share with anyone


### Connect to AWS from system terminal

* go to directory where key-pair is downloaded
* give permission to the key
	chmod 777 ec2-masterclass.pem
* Execute the following command
	ssh -i ec2-masterclass.pem ec2-user@`<public-ip-address>`


### Stop or Terminate the instance






