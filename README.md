# JENKINS CICD PIPELINE


Step 1 – Create the Ec2 instance in AWS account with these parameters
--------
    - EC2 type – Ubuntu t2.medium
    - EBS volume – 30 GB 
    - Region -AP SOUTH 1

<img width="800" height="300" src="https://github.com/tohidhanfi20/Java_app_3.0/blob/main/Screenshot's/step1.png)">

Step 2 – Connect to EC2 and Install all tools in that system as root user
-------

    - To login as root user - sudo su

Step 3 – Install Jenkins on Ubuntu
-------
 
   -  Just copy paste the entire command
     
    sudo apt update -y

    sudo apt upgrade -y 

    sudo apt install openjdk-17-jre -y

    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    
    sudo apt-get update -y 
    
    sudo apt-get install jenkins -y


Step 4 – Change the security group of ec2 instance
-------
 
    -  All traffic
    - Anywhere IPV4

Step 5 – Sign Into Jenkins console 
-------

    - http://<EC2_PUBLIC_IP>:8080/    

Step 6 – Get the Administrator password by hitting the below command in EC2    
-------

    - cat/var/lib/jenkins/secrets/initialAdminPassword

Step 7 – Install all suggested Plugins
-------

Step 8 – Create first user
-------

Step9 – Create a pipeline Job
-------

Step 10 – Add pipeline script as SCM
-------

    - https://github.com/tohidhanfi20/Java_app_3.0   

Step 11 – Add the Plugins
Dashboard -> Manage Jenkins -> Plugins -> Available plugins
-------

    - Plugins for Sonar/Jfrog
    – Sonar Gerrit 
    - SonarQube Scanner
    - SonarQube Generic Coverage 
    - Sonar Quality Gates 
    - Quality Gates 
    - Artifactory
    - Jfrog

Step 12 – Setup Docker
---------

-  Just copy paste the entire command

       - sudo apt update -y

         sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

         curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

         sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" -y

         sudo apt update -y

         apt-cache policy docker-ce -y

         sudo apt install docker-ce -y

         sudo systemctl status docker

         sudo chmod 777 /var/run/docker.sock

Step 13 - Install SonarQube
--------

         -  docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

Step 13.1 -> Start docker container if it's not up   
--------
      - docker ps -a [Get the container ID]
      - docker start <containerID>
Step 13.2 -> Log in into sonar dashboard  

      - Username – admin
      - Password – admin

Step 13.3 -> Create Sonar token for Jenkin 
---------

Sonar Dashboard -> Top right corner -> MyAccount -> Security -> Create token -> Save the token to some text file


Step 13.4 -> Integrate Sonar to Jenkins
---------

Sonar Dashboard -> Administration -> Configuration -> webhooks -> Add the below name and url and save

        - http://<EC2_IP>:8080/sonarqube-webhook/

Step 14 – Install Maven
---------

- Just copy paste the entire command

        - sudo apt update -y
          sudo apt install maven -y
          mvn -version

Step 15 – Install TRIVY for docker image scan  
----------

   - Just copy paste the entire command

   - A Simple and Comprehensive Vulnerability Scanner for Containers and other Artifacts, Suitable for CI.

         - sudo apt-get install wget apt-transport-https gnupg lsb-release
           wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
           echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
           sudo apt-get update
           sudo apt-get install trivy

Step 16 - Integrate All tools with Jenkins  
-------

Jenkins Dashboard -> Manage Jenkins -> configure system

Step 17 – ADD SONARQUBE
--------

Step 17.1 -> Click on sonarqube servers -> add url and name -> Click on add token -> Select Secret text -> Add the sonar token from 
---------

step13.3 -> Give name of token as sonarqube-api

Step 18 - Add the docker HUB credentials ID
---------

jenkins dashboard -> Manage Jenkins -> Credentials -> System -> click on global credentials

ADD the docker hub credentials with name as docker

Step 19 – Add the Jenkins Shared library
---------

Go to Manage Jenkins -> Configure system -> Global pipeline library -> Add below data Name -my-shared-library Default version – main

git - https://github.com/tohidhanfi20/jenkins_shared_lib

Step 20 - Once pipeline is Run Check 
---------

    - The Jenkins logs
    - The Trivy scan vulnerabilities 
    - The sonarqube dashboard for report
