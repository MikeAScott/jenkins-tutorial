# Learning Jenkins 
Use Jenkins to build and deploy applications and infrastructure

The link on the headings wil take you to the branch or tag for the lab.

For official Jenkins information goto https://www.jenkins.io/
  

In particular the [Jenkins Handbook](https://www.jenkins.io/doc/book/) is a good place to start.

For these labs we will install Jenkins in Docker in Virtual box using Vagrant

# [LAB-01](../../tree/LAB-01) - Set up Jenkins in Docker in Virtualbox
## Install Docker
* Install Virtualbox 
* Install Vagrant
* Have a look at the [Vagrantfile](Vagrantfile)
    * The provisioner sets up docker and docker compose in Ubuntu
* Run vagrant
```
vagrant up
```
* ssh to jenkins box
```
vagrant ssh jenkins
docker version
```
You should see the docker version page :)

## Setup Jenkins docker containers
* Have a look at the [docker-compose.yml](docker-compose.yml) file
  * This creates two services:
    * jenkins-docker: Runs the docker in docker service to allow running docker containers from Jenkimns
    * jenkins-blueocean: Runs the Jenkins server    
* Run docker compose to start the services
``` bash
docker-compose up -d
```

## Setup jenkins
* Open a browser on the Jenkins site https://localhost:8081
* Check the docker logs from the jenkins-blueocean service for the initial admin password
``` bash
docker logs jenkins-blueocean
```
* The output should contain the autogenerated password after the line:
  * `Please use the following password to proceed to installation:`
* Use this password to unlock jenkins
* Install the suggested plugins
* Create a first admin user
* Start using Jenkins


---
Free to use under [MIT Licence](./LICENCE)

Copyright (c) Mike Scott 2020
