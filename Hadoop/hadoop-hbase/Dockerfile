FROM dongqing/hadoop-base:1.0.0

MAINTAINER Dongqing

ADD Hadoop/hadoop-env.sh $HADOOP_HOME/etc/hadoop/
ADD Hadoop/mapred-env.sh $HADOOP_HOME/etc/hadoop/
ADD Hadoop/yarn-env.sh $HADOOP_HOME/etc/hadoop/
ADD Hadoop/core-site.xml $HADOOP_HOME/etc/hadoop/
ADD Hadoop/hdfs-site.xml $HADOOP_HOME/etc/hadoop/
ADD Hadoop/mapred-site.xml $HADOOP_HOME/etc/hadoop/
ADD Hadoop/yarn-site.xml $HADOOP_HOME/etc/hadoop/
ADD Hadoop/slaves $HADOOP_HOME/etc/hadoop/
ADD HBase/hbase-env.sh $HBASE_HOME/conf/
ADD hadoop-hbase/hbase-site.xml $HBASE_HOME/conf/
ADD hadoop-hbase/regionservers $HBASE_HOME/conf/

USER hadoop
RUN sudo mkdir -p /opt/hadoop/data/zookeeper
RUN sudo chown -R hadoop:hadoop $HADOOP_HOME/etc/hadoop
RUN sudo chown -R hadoop:hadoop $HBASE_HOME/conf
RUN sudo chown -R hadoop:hadoop /opt/hadoop
RUN sudo chown -R hadoop:hadoop /home/hadoop

RUN /usr/local/hadoop/bin/hdfs namenode -format

CMD ["sh", "-c", "sudo service sshd start;bash"]
