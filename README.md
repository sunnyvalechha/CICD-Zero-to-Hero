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

Launch aws instance with t2.medium (amazon 5.10 kernel)

* Install java 11 for amazon linux:
* sudo yum install java-11-amazon-corretto-headless -y
* java --version

Install maven: 
* https://downloads.apache.org/maven/
* cd /optwget https://downloads.apache.org/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.tar.gz
* tar xvf a
* pache-maven-3.8.8-bin.tar.gz
* export PATH=$PATH:/opt/apache-maven-3.8.8/bin
* mvn --version

Install git:
* yum install git -y
* git clone https://github.com/Shikhar82/springboot-webapplication.git

* cd /root/maven-project/springboot-webapplication
* mvn package (build package)
* cd /root/maven-project/springboot-webapplication/target (see the type of file .war .jar)
