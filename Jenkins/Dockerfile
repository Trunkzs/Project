FROM jenkins/jenkins:lts-jdk17

#ENV

USER root

RUN mkdir /opt/result/ \
    && mkdir /opt/reports 
# Install requirements
RUN apt-get update && \
    apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common \
    lsb-release # Install lsb-release package
# Install Docker
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io

# Install Docker Compose
RUN curl -L "https://github.com/docker/compose/releases/download/v2.13.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

# Install plugins
RUN jenkins-plugin-cli \
    --plugins \
    workflow-aggregator \
    blueocean \
    htmlpublisher \
    slack
      