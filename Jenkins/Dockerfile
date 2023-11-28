FROM jenkins/jenkins:lts-jdk17

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
    htmlpublisher
      