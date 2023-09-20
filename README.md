# Deploy with docker

### About the repository

This repository contains files and sample web application for building a dockerized application.  

#### Introduction

![Static Badge](https://img.shields.io/badge/Docker-blue) is a containerization tool which bundles our application codes and it's dependencies together to form an docker image which we can run as a container on the hosts machine. Docker made the application development ease and consistent.
In this project docker is used to build the appplication, then pushed to docker hub which is a repository for docker images where we can easily access our application image at our will. atlast ![Static Badge](https://img.shields.io/badge/Ansible-8A2BE2)is used for deployment in the server. All these process is automated by CI tool ![Static Badge](https://img.shields.io/badge/Jenkins-green)

#### Pre-requisities 

 - I downloaded a sample html web page from [opensourcetemplate](https://opensourcetemplates.org/)
 - Deployment server is configured with required applications like docker.
 - Jenkins controller is installed my local machine with plugins Git, docker pipeline etc..
 - Also make sure you have docker and ansible in your machine where you perform the CI CD with jenkins
 - Store the docker hub username and password as username and password type in jenkins credentials.
 - Store the private key of the server as secret file type in jenkins credentials.

 #### Description

  - In the repository, Inside the codebase directory we have our sample application code in the hills directory
  - Dockerfile is provided with Alpine Nginx as the base image ( this lightweight image is enough for our sample code). 
  - Ansible deployment files are present in the ansible directory. take a look at it.
  - Jenkinsfile contains the following stages:
    - First we build the image in the same name as ourr dockerhub repo
    - Second push the image to the dockerhub repo - the credentials can be accessed by the with credentials block
    - Ansible playbook does the deployment. The private key for the Ec2 instance accessed by the Environment variable.

### How to tweak it

If you want to try the same procedure like building the docker image and deploying to the server. Clone the repo, change the credentials with your own actual values. Also change the **ansible_hosts** of the server in the Ansible/invnetory file. It will work for you.
