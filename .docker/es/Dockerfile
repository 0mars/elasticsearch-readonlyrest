FROM docker.elastic.co/elasticsearch/elasticsearch:6.8.3

USER root
RUN cd /tmp \
    && yum install wget curl -y \
    && wget https://www.dropbox.com/s/qqcetmfihnkrqen/readonlyrest-1.18.7_es6.8.3.zip?dl=0 -O readonlyrest-plugin.zip \
    && chmod 777 /tmp/readonlyrest-plugin.zip \
    && chown elasticsearch:elasticsearch /tmp/readonlyrest-plugin.zip \
    && yum remove wget -y \
    && yum clean all -y

USER elasticsearch

RUN cd /usr/share/elasticsearch \
    && bin/elasticsearch-plugin install -b file:///tmp/readonlyrest-plugin.zip \
    && rm -f /tmp/readonlyrest-plugin.zip

ADD ./elasticsearch.yml /usr/share/elasticsearch/config/
ADD ./readonlyrest.yml /usr/share/elasticsearch/config/

EXPOSE 9200 9300
