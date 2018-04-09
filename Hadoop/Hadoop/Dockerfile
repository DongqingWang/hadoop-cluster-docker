FROM dongqing/hadoop-base:1.0.0

MAINTAINER Dongqing

ADD hadoop-env.sh $HADOOP_HOME/etc/hadoop/
ADD mapred-env.sh $HADOOP_HOME/etc/hadoop/
ADD yarn-env.sh $HADOOP_HOME/etc/hadoop/
ADD core-site.xml $HADOOP_HOME/etc/hadoop/
ADD hdfs-site.xml $HADOOP_HOME/etc/hadoop/
ADD mapred-site.xml $HADOOP_HOME/etc/hadoop/
ADD yarn-site.xml $HADOOP_HOME/etc/hadoop/
ADD slaves $HADOOP_HOME/etc/hadoop/

USER hadoop
RUN sudo mkdir -p /opt/hadoop/data/zookeeper
RUN sudo chown -R hadoop:hadoop $HADOOP_HOME/etc/hadoop
RUN sudo chown -R hadoop:hadoop /opt/hadoop
RUN sudo chown -R hadoop:hadoop /home/hadoop

RUN /usr/local/hadoop/bin/hdfs namenode -format

CMD ["sh", "-c", "sudo service sshd start;bash"]
