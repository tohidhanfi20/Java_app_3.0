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
