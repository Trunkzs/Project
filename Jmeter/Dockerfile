# inspired by https://github.com/hauptmedia/docker-jmeter  and
# https://github.com/hhcordero/docker-jmeter-server/blob/master/Dockerfile
FROM alpine:3.12

ARG JMETER_VERSION="5.6.2"
ENV JMETER_HOME /opt/apache-jmeter-${JMETER_VERSION}
ENV JMETER_BIN ${JMETER_HOME}/bin
ENV JMETER_DOWNLOAD_URL  https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz
ENV JMETER /opt/apache-jmeter-${JMETER_VERSION}/bin/jmeter

# Install extra packages
# Set TimeZone, See: https://github.com/gliderlabs/docker-alpine/issues/136#issuecomment-612751142
ARG TZ="Asia/Bangkok"
ENV TZ ${TZ}
RUN    apk update \
        && apk upgrade \
        && apk add ca-certificates \
        && update-ca-certificates \
        && apk add --update openjdk8-jre tzdata curl unzip bash vim git \
        && apk add --no-cache nss \
        && rm -rf /var/cache/apk/* \
        && mkdir -p /tmp/dependencies  \
        && curl -L  ${JMETER_DOWNLOAD_URL} >  /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz  \
        && mkdir -p /opt  \
        && tar -xzf /tmp/dependencies/apache-jmeter-${JMETER_VERSION}.tgz -C /opt  \
        && rm -rf /tmp/dependencies \
    && mkdir /opt/reports && mkdir /opt/result

# TODO: plugins (later)
