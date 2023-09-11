# DevOps-Project-1
In this project, we will explore how to set up a Jenkins CI/CD pipeline using Github, and Docker on an AWS EC2 instance.
# Project Overview :-
In this project I will create an AWS EC2 instance and install java then Jenkins on it. We will then set up a Github repository and integrate it with Jenkins. Finally, we will create a Docker image of our application and deploy it using Jenkins.
# Project Steps :-
Create 1 ec2 instance :
Jenkins-Server : AWS Ubuntu, t2.micro

![Screenshot 2023-09-08 142943](https://github.com/saaimazam/DevOps-Project-1/assets/125339535/fe454880-e9d2-4792-933f-b8b5e9b0025d)

# 1. Install and Configure Java & Jenkins :-
```bash
sudo apt update
```
- Java installation :-
```bash
sudo apt install openjdk-11-jre
java -version
```

- Package Installation for Jenkins :-
```bash
curl -fsSL https://pkg.jenkins.io/debian/jenkins.io.key | sudo tee \   /usr/share/keyrings/jenkins-keyring.asc > /dev/null 
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \   https://pkg.jenkins.io/debian binary/ | sudo tee \   /etc/apt/sources.list.d/jenkins.list > /dev/null
```
- Install, Enable and Start Jenkins :-
```bash
sudo apt-get update 
sudo apt-get install jenkins
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

