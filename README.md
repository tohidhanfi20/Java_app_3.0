Step 1 – Create the Ec2 instance in AWS account with these parameters
--------
    - EC2 type – Ubuntu t2.medium
    - EBS volume – 30 GB 
    - Region - US EAST 1

image

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

    - http://<EC2_PUBLIC_IP>:8080/    

Step 6 – Get the Administrator password by hitting the below command in EC2    

    - cat/var/lib/jenkins/secrets/initialAdminPassword

Step 7 – Install all suggested Plugins

Step 8 – Create first user

Step9* – Create a pipeline Job

Step 10 – Add pipeline script as SCM

    - https://github.com/tohidhanfi20/Java_app_3.0   

Step 11 – Add the Plugins
Dashboard -> Manage Jenkins -> Plugins -> Available plugins

    - Plugins for Sonar/Jfrog
    – Sonar Gerrit 
    - SonarQube Scanner
    - SonarQube Generic Coverage 
    - Sonar Quality Gates 
    - Quality Gates 
    - Artifactory
    - Jfrog

Step 12 – Setup Docker

-  Just copy paste the entire command

       - sudo apt update -y

         sudo apt install apt-transport-https ca-certificates curl software-properties-common -y

         curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

         sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" -y

         sudo apt update -y

         apt-cache policy docker-ce -y

         sudo apt install docker-ce -y

   #sudo systemctl status docker

         sudo chmod 777 /var/run/docker.sock




     
# kubernetes-configmap-reload

Pre-requisites:
--------
    - Install Git
    - Install Maven
    - Install Docker
    - EKS Cluster
    
Clone code from github:
-------
    git clone https://github.com/tohidhanfi20/Java_app_3.0
    cd spring-cloud-kubernetes/kubernetes-configmap-reload
    
Build Maven Artifact:
-------
    mvn clean install
 
Build Docker image for Springboot Application
--------------
    docker build -t vikashashoke/kubernetes-configmap-reload .
  
Docker login
-------------
    docker login
    
Push docker image to dockerhub
-----------
    docker push vikashashoke/kubernetes-configmap-reload
    
Deploy Spring Application:
--------
    kubectl apply -f kubernetes-configmap.yml
    
Check Deployments, Pods and Services:
-------

    kubectl get deploy
    kubectl get pods
    kubectl get svc
    
Now Goto Loadbalancer and check whether service comes Inservice or not, If it comes Inservice copy DNS Name of Loadbalancer and Give in WebUI

    http://a70a89c22e06f49f3ba2b3270e974e29-1311314938.us-west-2.elb.amazonaws.com:8080/home/data
    
![2](https://user-images.githubusercontent.com/63221837/82123471-44f5f300-97b7-11ea-9d10-438cf9cc98a0.png)

Now we can cleanup by using below commands:
--------
    kubectl delete deploy kubernetes-configmap-reload
    kubectl delete svc kubernetes-configmap-reload
# springboot_k8s_application
# mrdevops_java_app
# Java_app_3.0
# Java_app_3.0
