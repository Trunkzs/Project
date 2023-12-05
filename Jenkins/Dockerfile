FROM docker pull jenkins/jenkins:2.426-jdk17

#ENV

USER root

RUN mkdir /opt/result/ \
    && mkdir /opt/reports 
# Install plugins
RUN jenkins-plugin-cli \
    --plugins \
    git \
    workflow-aggregator \
    blueocean \
    htmlpublisher \
    slack
      