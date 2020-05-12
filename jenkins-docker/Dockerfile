FROM jenkins/jenkins:lts

USER root
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common 
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

# Set Docker group id so it can be mapped from host 
ARG DOCKER_GID=300
RUN groupadd -g ${DOCKER_GID} docker

RUN apt-get update  -qq \
    && apt-get install docker-ce-cli -y

RUN usermod -aG docker jenkins
# RUN touch /var/run/docker.sock \
#   && chown :docker /var/run/docker.sock
USER jenkins