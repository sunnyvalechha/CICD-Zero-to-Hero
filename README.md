# Maven

* Maven is a Java Project management tool.
* It is also called as build tool or manage dependencies.
* It is an automation tool developed by Apache software. It is based on POM file (Project object model) also pom.xml
* POM consist dependencies and compiler details which required to build a project. Pom contains following things:
  1. Metadata
  2. Dependencies
  3. Kind of Project
  4. Kind of Output (.jar .war)
  5. Description
  6. Versioning management
    
* One Pom file has only 1 project and has one Workspace.
* Maven can build project into desired format like .jar / .war
* Maven is written in java

# Maven Life Cycle

1. Generate resources (dependencies).
2. Compile Code.
3. Unit test
4. Package build
5. maven install into Local repository
6. Deploy to servers
7. maven clean (delete all runtime files)

**Maven directory structure**

![image](https://github.com/sunnyvalechha/CICD-Zero-to-Hero/assets/59471885/69402cbb-601a-447d-865d-a27dff7152d3)

**Practical for Maven**

1. Launch aws instance with t2.medium (amazon 5.10 kernel)

2. Install java 11 for amazon linux: URL: https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/amazon-linux-install.html

3. sudo yum install java-11-amazon-corretto-headless -y

4. java --version

5. Install maven:
   	https://downloads.apache.org/maven/
	cd /opt
	sudo wget https://downloads.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz
	sudo tar xvf apache-maven-3.8.8-bin.tar.gz
	export PATH=$PATH:/opt/apache-maven-3.8.8/bin
	echo $PATH
	sudo yum install maven -y
	mvn --version

7. Install git:
	mkdir maven-project/
	cd maven-project/
	sudo yum install git -y
	git clone https://github.com/Shikhar82/springboot-webapplication.git
	cd /root/maven-project/springboot-webapplication
	mvn package (build package)
	cd /root/maven-project/springboot-webapplication/target (see the type of file .war .jar)

# SonarQube

* Code quality of the build can be checked by the Sonarqube.
* SonarQube is a self-managed, automatic code review tool that systematically helps you deliver Clean Code. SonarQube integrates into your existing workflow and detects issues in your code to help you perform continuous code inspections of your projects.
* Sonar works on port number 9000

![image](https://github.com/sunnyvalechha/CICD-Zero-to-Hero/assets/59471885/656f338a-a294-45db-a94b-626d2e57dfb5)

**Practical for Sonar**

1. Install Sonarqube:
	Launch ubuntu instance with t2.medium

2. Install OpenJDK URL: https://www.linode.com/docs/guides/how-to-install-openjdk-on-ubuntu-20-04/

sudo apt install openjdk-11-jre-headless -y
sudo apt install openjdk-11-jdk-headless -y

Sonar verson 9.3


Open port 9000 in Sec group.

Open Website > Downloads > Copy link (click here)
cd /opt

wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.5.1.90531.zip?_gl=1*1hx7cy0*_gcl_au*MTc2NzUwMTUzMi4xNzE3OTI0MjU4*_ga*NjM2MzkzOC4xNzE3OTI0MjU1*_ga_9JZ0GZ5TC6*MTcxODA4NzUwMS4zLjEuMTcxODA4Nzg5MC42MC4wLjA.

apt install unzip -y

unzip https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-10.5.1.90531.zip?_gl=1*1hx7cy0*_gcl_au*MTc2NzUwMTUzMi4xNzE3OTI0MjU4*_ga*NjM2MzkzOC4xNzE3OTI0MjU1*_ga_9JZ0GZ5TC6*MTcxODA4NzUwMS4zLjEuMTcxODA4Nzg5MC42MC4wLjA.

Note: Go back to regular user like ubuntu, it is not recomended to user root user in sonarqube beacuse in backend sonarqube use elastic search and it is not recomended to use ES with root user.

/opt/sonarqube-10.5.1.90531/bin/linux-x86-64
sh sonar.sh

Note: If get an error that we are running is as root and script not ran.

vim sonar.sh
RUN_AS_USER=ubuntu

sh sonar.sh start (If again get failed, change ownership of some files)

cd /opt
sudo apt install acl -y
getfacl sonarqube
chown ubuntu: sonarqube/ -R

sh sonar.sh status

Google: PublicIP:9000

Username/Pass: admin

# Integrate Sonar with Maven

Google: maven sonar integration > Sonar scanner for maven > How to fix version of maven plugin

copy from 2nd <plugin> to 2nd last <plugin> keep in notepad

check current version of sonar maven scanner ?

Google: Sonar maven scanner > org.sonarsource > 3.9.1.2184 and replace the version in notepad

How sonar qube know that we need to check the code from maven ?
for this we need to generate token

Sonar qube > my account > security > give name (sonar-token) generate token > copy to notepad

mvn sonar:sonar -Dsonar.host.url=http://<publicIp>:9000 -Dsonar.login=<token of sonar> 

file above command at maven server inside the clone repository dirctory

* Go to Sonar > Projects > (we can see real time projects)

Will do some errors in code

cd src/main/java/com/cloud/realtime

vim customercontroller
@GetMapping {
System.out.println("getAllCustomers is called by /getAllCustomers");

Go to source repo again > maven clean package
run the token command again to recheck the code (failed)

correct it > Google: spring boot sl4j example
hello logback > 

import org.slf4j>looger
import org.slf4j.Logger

private static final Logger logger (CustomerController.class)  #change this line in file

cd src/main/java/com/cloud/realtime
vim customercontroller

paste > below 3rd line import 
