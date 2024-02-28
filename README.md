# Jenkins-pipeline-installation-to-build
About this project. To Install Jenkins, configure Docker as slave/agent set up cicd, and deploy applications to k8s using Argo CD in GitOps way

Install Jenkins, configure Docker as agent, set up cicd, and deploy applications to k8s.

      steps1-AWS EC2 Instance
Create-Instance in AWS EC2
Launch instancesGo 
to AWS Console
make sure Instances(running)
Using public IP address ssh -i to the EC2 instance (server VM)

STEP2 Install Jenkins (before installition run apt update to updated the packages and then install JDK)

Pre-Requisites:
Java (JDK)

Run the below commands to install Java and Jenkins
Install Java

udo apt install openjdk-11-jre

Verify Java is Installed
java -version

Now, you can proceed with installing Jenkins

curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

**Note: ** By default, Jenkins will not accept any traffic to be accessible to the external world this is beacuse the inbound traffic is (blocked) is restricted by AWS (defult).

To see or check the port jenkins is running into 
run  ps -ef | grep jenkins      to see port 8080

So port 8080 is not acceble to extenal world since traffic is been restricted.
To access/ Open port 8080 go to security in ec2 instance than click on security group then clik on edit in inbound rules as show below.
