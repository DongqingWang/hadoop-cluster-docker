FROM centos:6
MAINTAINER Dongqing

RUN yum -y update
RUN yum install -y openssh-server openssh-clients sudo which initscripts wget java-1.8.0-openjdk

RUN groupadd hadoop
RUN useradd -m hadoop -g hadoop -p hadoop

ENV JAVA_HOME=/usr/lib/jvm/jre

ENV CLASSPATH=.:$JAVA_HOME/lib/rt.jar

ENV PATH=$PATH:$JAVA_HOME/bin

RUN wget -c http://www-eu.apache.org/dist/hadoop/common/hadoop-2.7.5/hadoop-2.7.5.tar.gz -P /tmp
RUN cd /usr/local/ && tar -zxvf /tmp/hadoop-2.7.5.tar.gz

RUN chown -R hadoop:hadoop /usr/local/hadoop-2.7.5
RUN cd /usr/local/ && ln -s ./hadoop-2.7.5 hadoop && rm -f ./hadoop-2.7.5.tar.gz

ENV HADOOP_PREFIX /usr/local/hadoop
ENV HADOOP_HOME /usr/local/hadoop
ENV HADOOP_COMMON_HOME /usr/local/hadoop
ENV HADOOP_HDFS_HOME /usr/local/hadoop
ENV HADOOP_MAPRED_HOME /usr/local/hadoop
ENV HADOOP_YARN_HOME /usr/local/hadoop
ENV HADOOP_CONF_DIR /usr/local/hadoop/etc/hadoop
ENV PATH ${HADOOP_HOME}/bin:$PATH

RUN wget -c http://www-eu.apache.org/dist/hbase/stable/hbase-1.2.6-bin.tar.gz -P /tmp
RUN cd /usr/local/ && tar -zxvf /tmp/hbase-1.2.6-bin.tar.gz

RUN chown -R hadoop:hadoop /usr/local/hbase-1.2.6
RUN cd /usr/local/ && ln -s ./hbase-1.2.6 hbase && rm -f ./hbase-1.2.6-bin.tar.gz

ENV HBASE_HOME /usr/local/hbase
ENV PATH ${HBASE_HOME}/bin:$PATH

RUN cd /etc/sudoers.d && sudo touch nopasswdsudo && echo "hadoop ALL=(ALL) NOPASSWD : ALL" >> nopasswdsudo

RUN mkdir /var/run/sshd

USER hadoop

RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
RUN  echo "StrictHostKeyChecking=no" > ~/.ssh/config && \
     echo "UserKnownHostsFile=/dev/null" >> ~/.ssh/config
CMD ["/bin/bash"]

EXPOSE 22
