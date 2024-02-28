# Jenkins-pipeline-installation-to-build
About this project. To Install Jenkins, configure Docker as slave/agent set up cicd, and deploy applications to k8s using Argo CD in GitOps way

Install Jenkins, configure Docker as agent, set up cicd, and deploy applications to k8s.

      steps1-AWS EC2 Instance
Create-Instance in AWS EC2
Launch instancesGo 
to AWS Console
make sure Instances(running)
Using public IP address ssh -i to the EC2 instance (CLI VM)

STEP2 Install Jenkins (before installition run apt update to updated the packages and then install JDK)

Pre-Requisites:
Java (JDK)

Run the below commands to install Java and Jenkins
Install Java

sudo apt updateVerify Java is Installed

java -version
sudo apt install openjdk-11-jre


