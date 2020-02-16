### Create Elastic IP address

* Go to Elastic IP Features in EC2 
* Allocate new Address
* Select a network Border Group
* select Amazon pool
* Allocate

### Host a EC2 instance using the AMI 
* Install a EC2 instance using the AMI as mentioned in [create AMI](https://github.com/konman01/AWS/tree/master/EC2/create-ami)

### Attach the EC2 instance to the Elastic IP
* Go to Elastic IP Features in EC2 
* Select the Elastic Ip Address created earlier
* Go to action and select the associate Address
* Then select the instance and its private address
