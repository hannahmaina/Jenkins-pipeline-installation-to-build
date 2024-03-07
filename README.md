
****Jenkins-pipeline-installation-to-build
About this project. To Install Jenkins, configure Docker as slave/agent set up cicd, and deploy applications to k8s using Argo CD in GitOps way

....,Install Jenkins, configure Docker as agent, set up cicd, and deploy applications to k8s.

steps1-AWS EC2 Instance
Create-Instance in AWS EC2
Launch instancesGo 
to AWS Console
make sure Instances(running)
Using public IP address ssh -i to the EC2 instance (server VM)

****Install Jenkins (before installition run apt update to updated the packages and then install JDK)

Pre-Requisites:
Java (JDK)

****Run the below commands to install Java and Jenkins
Install Java
```
udo apt install openjdk-11-jre
```
****Verify Java is Installed

```
java -version
```

Now, you can proceed with installing Jenkins
````````````
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
`````````

**Note: ** By default, Jenkins will not accept any traffic to be accessible to the external world this is beacuse the inbound traffic is (blocked) is restricted by AWS (defult).

****To see or check the port jenkins is running into 
`````
run  ps -ef | grep jenkins      to see port 8080
``````

****So port 8080 is not acceble to extenal world since traffic is been restricted.
To access/ Open port 8080 

+. Go to EC2 > Instances > Click on
+.In the bottom tabs -> Click on Security
+.Then Click on Security groups
+.Click on edit inbound rules
+.Then Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic). click save



<img width="1187" alt="inbund traffic" src="https://github.com/hannahmaina/Jenkins-pipeline-installation-to-build/assets/112791368/04843d6b-e5d6-4d47-87e5-21f334784ea9"> 

****Login to Jenkins using the below URL:

+.http://:8080 [get your ec2-instance-public-ip-address from your AWS EC2 console page] to see if jenkins is accessble to extenal world or not
http://:8088 my pulic ip address


After I can change my inbound traffic rule if I want to to below
Note: If you are not interested in allowing All Traffic to your EC2 instance 1. Delete the inbound traffic rule for your instance 2. Edit the inbound traffic rule to only allow custom TCP port 8080

After you login to Jenkins, - Copy Jenkins Admin Password and run this commad in taminal 
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword (this is your Jenkins Admin password yoy copy)
````
![jenkpilog](https://github.com/hannahmaina/Jenkins-pipeline-installation-to-build/assets/112791368/5af0fafc-b05e-41a9-bfcf-da839b56a910)

****Install the Docker Pipeline plugin in Jenkins: So we can run docker as agent. Jeckins will understand if the user excuted job to run as a pipeline 

+.Log in to Jenkins.
+.Go to Manage Jenkins > Manage Plugins.
+.In the Available tab, search for "Docker Pipeline". in Jenkins
+.Select the plugin and click the Install button.
+.Restart Jenkins after the plugin is installed.

****Docker Slave Configuration
+.Run the below command to Install Docker
````
sudo apt update
sudo apt install docker.io
``````

****Grant Jenkins user and Ubuntu user permission to docker deamon.
````
sudo su - jenkins to login to jenkins in terminal
``
usermod -aG docker jenkins   (this is to give access to jenkins -makes Jenkins to be part of docker group)
usermod -aG docker ubuntu     (gives access to user docker demons)
systemctl restart docker     (this is to restart docker demons)
````
I terminal run command
s
****Once you are done with the above steps, better to restart Jenkins. so restart
``
http://<ec2-instance-public-ip>:8080/restart
```
Now docker agent configuration is now successful install in jenkins plugins and taminal

+. Now i can write my first pipeline











