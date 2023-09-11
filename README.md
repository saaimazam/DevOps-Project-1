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
- Copy public ip of jenkins server and paste it in new tab with port no.8080
![Screenshot 2023-09-11 122125](https://github.com/saaimazam/DevOps-Project-1/assets/125339535/166f51e3-426b-4ca9-9840-19b65e3c3be5)

- copy this path and paste in terminal with "cat" command
```bash
cat /var/lib/jenkins/secrets/initialAdminPassword
```
- Now copy & paste this passwd in jenkins. so, jenkins is ready.

# 2. Run the code in jenkins:
- Jenkins-> New Item-> Freestyle Project-> Source Code Management-> Git
![image](https://github.com/saaimazam/DevOps-Project-1/assets/125339535/8f290ed2-a0bb-4d94-a60b-6b3dbea0de06)


- Connect github to jenkins through webhook

![image](https://github.com/saaimazam/DevOps-Project-1/assets/125339535/504d78c0-7637-4b40-900a-b14615bb8a95)

- Build Now in Jenkins

![Screenshot 2023-09-08 142849](https://github.com/saaimazam/DevOps-Project-1/assets/125339535/a02690bc-91ef-472c-afe4-cb9be6681f43)

# 3. Connect to terminal and install docker :-

```bash
sudo apt-get update
```
- Install docker
```bash
sudo apt install docker.io
```
- Lets Integrate Docker with Jenkins
- Jenkins -> Manage Jenkins -> Plugins -> Available -> Search for Publish Over SSH -> Install
- Lets configure Docker in Jenkins
- Jenkins -> Manage Jenkins -> System -> Publish Over SSH -> SSH Servers -> Add -> Give Name -> Hostname : -> Username : dockeradmin -> advanced -> enable password based authentication -> password : <password of dockeradmin -> test configuration -> Apply -> Save
- Successfully instegrated docker with jenkins.
- Now goto docker server

# 4. Create and run docker file
- Goto the directory where application code is clone.
- Create a docker file
```bash
vim Dockerfile
```
- Write code in the docker file
```bash
FROM node:12.2.0-alpine
WORKDIR app
COPY . .
RUN npm install
EXPOSE 8000
CMD ["node","app.js"]
```

- Now, build the file.
```bash
docker build . -t node-app
```
- Grant user permissions.
```bash
sudo usermod -a -G docker $USER
```
- After that, run docker image as a container.
```bash
docker run -d --name node-todo-app -p 8000:8000 todo-node-app
```

# Run app with Jenkins
- Goto Jenkins Job > Free style project > Add git repository > Build steps > Execute shell

- In the execute shell right these commands 
```bash
FROM node:12.2.0-alpine
WORKDIR app
COPY . .
RUN npm install
EXPOSE 8000
CMD ["node","app.js"]
```

- Apply & Save

# App will run Successfully. 
