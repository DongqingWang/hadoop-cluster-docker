FROM centos:6
MAINTAINER Dongqing

RUN yum -y update
RUN yum install -y openssh-server openssh-clients sudo which initscripts

ADD jdk-8u162-linux-x64.rpm /tmp
RUN yum localinstall -y /tmp/jdk-8u162-linux-x64.rpm

RUN groupadd hadoop
RUN useradd -m hadoop -g hadoop -p hadoop

ADD hadoop-2.7.5.tar.gz /usr/local/

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

ADD hbase-1.2.6-bin.tar.gz /usr/local/

RUN chown -R hadoop:hadoop /usr/local/hbase-1.2.6
RUN cd /usr/local/ && ln -s ./hbase-1.2.6 hbase && rm -f ./hbase-1.2.6-bin.tar.gz && ls

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
