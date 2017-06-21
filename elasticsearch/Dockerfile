FROM docker.elastic.co/elasticsearch/elasticsearch:5.4.1

MAINTAINER WangChao POUTORD <watcher.hangzhou@foxmail.com>

RUN mkdir /usr/share/elasticsearch/plugins/ik
ADD ik /usr/share/elasticsearch/plugins/ik

# ADD elasticsearch.yml /usr/share/elasticsearch/config/

USER root
# RUN chown elasticsearch:elasticsearch config/elasticsearch.yml

RUN chown -Rf elasticsearch:elasticsearch /usr/share/elasticsearch/plugins/

USER elasticsearch
