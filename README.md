# kubernetes-2.1

Rolling out and Rolling back Deployments

1. Go to Spring Initializr.
2. Choose following configuration :
a. Project : Maven
b. Spring Boot : 2.7.3
c. Group name : com.star.agile.assignment
d. Name : springboot-demo
e. Artifact : springboot-demo
f. Packaging : Jar
g. Java : 8 or 11
3. In the dependency section, choose following dependency
a. Spring Web
b. Spring Data JPA
4. Click on Explore and verify the pom.xml that all the selected dependencies are present.
5. Click on download to download the Spring Boot Project Template. (springbootdemo.jar)
6. Import the downloaded project in Eclipse.
7. Add the file index.html with some HTML code in the static folder under resources of the Project.
8. Write the Dockerfile to create the image and tag it as 1.0.
9. Push the Image to Docker Hub.
10. Setup the Kubernetes minikube single node cluster on an AWS EC2 Ubuntu instance.

11. Write a deployment to deploy the application as POD using Kubectl.
12. Create the node port service to expose the deployed container to the outside world.
13. Verify the application over browser.
14. Add a Hello world.html to the Spring Boot Application.
15. Build the docker image and give the tag as 2.0 this time.
16. Roll out the deployment of the 2.0 version.
17. Verify the app that new version has been deployed.
18. Rollback the deployment to the old version.
19. Verify the version and try to access the helloworld.html, It should not be accessible anymore.

1. Go to Spring Initializr.
Link:- https://start.spring.io/

2. Choose following configuration :
a. Project : Maven
b. Spring Boot : 2.7.3
c. Group name : com.star.agile.assignment
d. Name : springboot-demo
e. Artifact : springboot-demo
f. Packaging : Jar
g. Java : 8 or 11

3. In the dependency section, choose following dependency
a. Spring Web
b. Spring Data JPA

4. Click on Explore and verify the pom.xml that all the selected dependencies are present.


<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.7.12</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.star.agile.assignment</groupId>
	<artifactId>springboot-demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>springboot-demo</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>1.8</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>





5. Click on download to download the Spring Boot Project Template. (springbootdemo.jar)


6. Import the downloaded project in Eclipse.
We first extract the file i.e:-

→ Now we will open our “Eclipse” 
→ Click on files & click on “Import”
→ Click on “Maven”
→ Click on “Existing Maven Project”

→ Click on “Next” 
→ Now click on “Browse” → goto the folder & select “springboot-demo”
→ Click on “Finish”

7. Add the file index.html with some HTML code in the static folder under resources of the project.



8. Write the Dockerfile to create the image and tag it as 1.0.
We will launch an Ubuntu instance in aws & access it through our terminal :- 

Now we update & upgrade the machine by using the command :- sudo apt-get update && apt-get upgrade -y
Now we install docker by using the command i.e :- sudo apt-get install docker.io -y
→ We can check the docker version by using the command i.e :- docker --version

→ To check the status, we use the command i.e :- systemctl status docker

→ Now we will install “Maven” by using command i.e :- sudo apt-get install maven -y
→ We can check the version by using command i.e :- mvn --version

→ Now in Eclipse we will create file as “Dockerfile” & here we will write 

FROM openjdk:8
EXPOSE 8080
ADD target/*.jar springboot-demo-1.0.jar
ENTRYPOINT ["java", "-jar", "/springboot-demo-1.0.jar"]

HERE WE HAVE UPLOADED OUR RESOURCES TO GitHub:-
→ Now we will Go to C:\Users\subha\Downloads\springboot-demo (1)\springboot-demo
→ Right click & select “GitBash here”
→ Now in “GitHub” we will create a New repository in the name of “kubernetes-2.1”
→ Now we use the “git init” command to initialize the directory.
→ To check unstaged files :- git status
→ Now we use the command i.e “git add .” command to add these files to the staging area.
→ Now we use the :-git commit -m “files for kubernetes-2.1 ”
→  Finally we will push the commit i.e :- git push -u origin master

Local folder

GitHub:-

Now we will clone our GitHub repository to our Docker instance i.e :- git clone https://github.com/sekhar-1995/kubernetes-2.1.git

To tag the image as 1.0:- docker build -t springboot-demo:1.0 .


9. Push the Image to Docker Hub.
We login to Docker Hub :- docker login

→ Now we will tag our image by using command i.e :- 
docker tag springboot-demo:1.0 subham742/springboot-demo:1.0
→ Now we will push our image to Docker Hub by using command i.e :- 
 docker push subham742/springboot-demo:1.0






→ Now we make a container from the image :- docker run -itd -p 8081:8080 springboot-demo:1.0

10. Setup the Kubernetes minikube(Kubeadm) single node cluster on an AWS EC2 Ubuntu instance.
→ Now we will launch a separate AWS instance(Node)  as “K8s-slave” with following Specification:-
Name :- K8s-slave
AMI:- Ubuntu 20.04LTS
Type :- t2.small
Security Group :- Port 22 (for SSH) from MyIP

On Master Node:-
When Instance get started successfully, we will open it using the Terminal by using the command i.e :- 
ssh -i star-jenkins.pem ubuntu@44.203.44.92 (here 44.203.44.92  is our Public IP)
→ Now we will become root user by using command i.e :- sudo -i
→ Now we will update & upgrade our machine by using the command i.e :- sudo apt-get update && apt-get upgrade -y

On Slave Node:-
When Instance get started successfully, we will open it using the Terminal by using the command i.e :- 
ssh -i star-jenkins.pem ubuntu@54.90.114.141 (here 54.90.114.141    is our Public IP)
→ Now we will become root user by using command i.e :- sudo -i
→ Now we will update & upgrade our machine by using the command i.e :- sudo apt-get update && apt-get upgrade -y

→ Now we will install “kubeadm in our ubuntu machine i.e Master Node & Slave Node” following the instruction available here:-
https://github.com/anujdevopslearn/InterviewQuestions/blob/master/InstallationGuides/Kubernetes.txt

We have to run following commands One by One on both “Master node & Slave node”:-
apt-get update && apt-get install -y curl apt-transport-https

sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update

sudo apt-get install -y containerd.io docker-ce 

curl -s https://packages.cloud.google.com/apt/doc/yum-key.gpg | apt-key add -

echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list

apt-get update

apt -y install kubeadm kubectl kubelet

#Open Below file and then comment disabled_plugin for CRI Runtime

vi /etc/containerd/config.toml    (Add # in front of disabled_plugin in this file and save it)

service containerd restart




To check kubeadm is installed :- kubeadm version 

Start the minikube (kubeadm) cluster. 
We have to run following commands One by One:-
(We have to use these commands only on “Master Node”)
kubeadm init

mkdir -p $HOME/.kube

sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubeadm token create --print-join-command

kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

(Here “ kubeadm init ” command is used to initialise/start the cluster)

Once all these done, we will copy the token from Master Node & paste it on the Slave Node i.e :- 


11. Write a deployment to deploy the application as POD using Kubectl.
For this we will create a file in the name of “demloyment.yml” :- vim deployment.yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: springboot-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: springboot-demo
  template:
    metadata:
      labels:
        app: springboot-demo
    spec:
      containers:
        - name: springboot-demo
          image: subham742/springboot-demo:1.0
          ports:
            - containerPort: 8080

→ Save & quit :- :wq


12. Create the node port service to expose the deployed container to the outside world.
For this we create a “service.yml” file & write :- vi service.yml
apiVersion: v1
kind: Service
metadata:
  name: springboot-demo-service
spec:
  selector:
    app: springboot-demo
  type: NodePort
  ports:
   - port: 8080
     targetPort: 8080
     nodePort: 30100

→ Save & exit :- :wq


13. Verify the application over browser.


14. Add a Hello world.html to the Spring Boot Application.
HelloWorld.html
<!DOCTYPE html>
<html lang="en">
 <head>
   <meta charset="utf-8">
   <title>My test page</title>
   <link href="http://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet" type="text/css">
   <link href="styles/style.css" rel="stylesheet" type="text/css">
 </head>
 <body>
   <h1>Hello From SUBHAM SEKHAR RATH</h1>
   <img src="images/firefox-icon.png" alt="The Firefox logo: a flaming fox surrounding the Earth.">
   <p>At Mozilla, we’re a global community of</p>
   <ul> <!-- changed to list in the tutorial -->
     <li>technologists</li>
     <li>thinkers</li>
     <li>builders</li>
   </ul>
   <p>working together to keep the Internet alive and accessible, so people worldwide can be informed contributors and creators of the Web. We believe this act of human collaboration across an open platform is essential to individual growth and our collective future.</p>
   <p>Read the <a href="https://www.mozilla.org/en-US/about/manifesto/">Mozilla Manifesto</a> to learn even more about the values and principles that guide the pursuit of our mission.</p>
 </body>
</html>




15. Build the docker image and give the tag as 2.0 this time.
→ Now we will Go to C:\Users\subha\Downloads\springboot-demo (1)\springboot-demo
→ Right click & select “GitBash here”
→ Now in “GitHub” we will create a New repository in the name of “kubernetes-2.1”
→ Now we use the “git init” command to initialize the directory.
→ To check unstaged files :- git status
→ Now we use the command i.e “git add .” command to add these files to the staging area.
→ Now we use the :-git commit -m “files for kubernetes-2.1 ”
→  Finally we will push the commit i.e :- git push -u origin master

Local folder

GitHub:-

Now we create a new directory in the name of “k8s-2.0” &  clone our GitHub repository to our Docker instance i.e :- 
git clone https://github.com/sekhar-1995/kubernetes-2.1.git

To tag the image as 2.0:- docker build -t springboot-demo:2.0 .


 Push the Image to Docker Hub.
We login to Docker Hub :- docker login

→ Now we will tag our image by using command i.e :- 
docker tag springboot-demo:2.0 subham742/springboot-demo:2.0
→ Now we will push our image to Docker Hub by using command i.e :- 
 docker push subham742/springboot-demo:2.0



→ Now we make a container from the image :- 


16. Roll out the deployment of the 2.0 version.
Update the deployment to use the new image version by running the following command:
kubectl set image deployment/springboot-demo springboot-demo=subham742/springboot-demo:2.0


17. Verify the app that a new version has been deployed.



Verify on WebBrowser:- 54.90.114.141 PublicIP of Node



18. Rollback the deployment to the old version.


19. Verify the version and try to access the helloworld.html, It should not be accessible anymore.

To check “HelloWorld.html” should not be accessible anymore.:-


