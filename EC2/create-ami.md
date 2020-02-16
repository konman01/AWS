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
	ssh -i ec2-masterclass.pem ec2-user@<public-ip-address>

### Execute the following commands to install the dependencies in the instance hosted

#### upgrade machine
sudo yum update -y

#### install java 8 jdk
sudo yum install -y java-1.8.0-openjdk-devel

#### set java jdk 8 as default
sudo /usr/sbin/alternatives --config java
sudo /usr/sbin/alternatives --config javac

#### verify java 8 is the default
java -version

#### Download app
cd /home/ec2-user
wget https://github.com/simplesteph/ec2-masterclass-sampleapp/releases/download/v1.0/ec2-masterclass-sample-app.jar

#### Test the app
java -Xmx700m -jar ec2-masterclass-sample-app.jar

#### Application will be stated and will running on port 4567

#### Add the port 4567 to the security group

Type: custom, protocol: tcp, port-range: 4567, source: anywhere, description: Java application running port

#### Application is available and can be accessed using the following URL

http://<ip address of the instance>:4567/

### Execute the following shell program to automatically install and host the Java application


#### long running configuration (persist after reboot)

#### write the ec2sampleapp file

sudo bash -c 'cat << \EOF > /etc/init.d/ec2sampleapp

# EC2 Sample App    Init script for EC2 Sample App
#
# chkconfig: 345 99 76
# processname: ec2sampleapp
#

APP_EXEC="/usr/bin/java -Xmx700m -jar /home/ec2-user/ec2-masterclass-sample-app.jar"
NAME=ec2sampleapp
PIDFILE=/var/run/$NAME.pid
LOG_FILE="/home/ec2-user/$NAME.log"
SCRIPTNAME=/etc/init.d/$NAME
RETVAL=0

start() {
    echo "Starting $NAME..."
    $APP_EXEC 1>"$LOG_FILE" 2>&1 &
    echo $! > "$PIDFILE"
    echo "$NAME started with pid $!"
}

status() {
    printf "%-50s" "Checking $NAME..."
    if [ -f $PIDFILE ]; then
        PID=$(cat $PIDFILE)
        if [ -z "$(ps axf | grep ${PID} | grep -v grep)" ]; then
            printf "Process dead but pidfile exists"
        else
            echo "Running"
        fi
    else
        printf "Service not running"
    fi
}

stop() {
    printf "%-50s" "Stopping $NAME"
        PID=`cat $PIDFILE`
    if [ -f $PIDFILE ]; then
        kill -HUP $PID
        printf "%s\n" "Ok"
        rm -f $PIDFILE
    else
        printf "%s\n" "pidfile not found"
    fi
}

case "$1" in
    start)
    start
    ;;
    status)
    status
    ;;
    stop)
    stop
    ;;
    restart)
        $0 stop
        $0 start
    ;;
    *)
        echo "Usage: $0 {status|start|stop|restart}"
        exit 1
    ;;
esac
EOF'


### Give permissions to start the file
sudo chmod +x /etc/init.d/ec2sampleapp

#### apply across reboots to automatically execute the script
* sudo chkconfig --add ec2sampleapp
* sudo chkconfig ec2sampleapp on

### Save the instance as an AMI
 * Go the instance
 * Select Action tab
 * Go to Image
 * Select create image

 This will create the AMI

### Host the instance using the AMI
 * Go to AMI section
 * Write click on the AMI created
 * Launch the instance


### The Java application will be hosted automatically to AWS which can be accssed using the public ip of the instance created using the AMI



### Stop or Terminate the instance