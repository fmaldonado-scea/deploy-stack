FROM ubuntu:trusty
MAINTAINER Felix Maldonado <felix_maldonado@playstation.sony.com>
LABEL Description="Fluentd to AWS Elasticsearch"

ENV DEBIAN_FRONTEND noninteractive

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get -y update
RUN apt-get -y install curl 

RUN /usr/bin/curl -L https://toolbelt.treasuredata.com/sh/install-ubuntu-trusty-td-agent2.sh | sh

RUN td-agent-gem install fluent-plugin-aws-elasticsearch-service
RUN td-agent-gem install fluent-plugin-s3

COPY ./td-agent.conf /etc/td-agent/td-agent.conf

ENV FLUENTD_CONF="td-agent.conf"

EXPOSE 24224

CMD /usr/sbin/td-agent -c /etc/td-agent/$FLUENTD_CONF
