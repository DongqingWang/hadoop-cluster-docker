FROM dongqing/hadoop-base:1.0.0

MAINTAINER Dongqing

ADD hbase-env.sh $HBASE_HOME/conf/
ADD hbase-site.xml $HBASE_HOME/conf/
ADD regionservers $HBASE_HOME/conf/

USER hadoop
RUN sudo mkdir -p /opt/hadoop/data/zookeeper
RUN sudo chown -R hadoop:hadoop $HBASE_HOME/conf
RUN sudo chown -R hadoop:hadoop /opt/hadoop
RUN sudo chown -R hadoop:hadoop /home/hadoop


CMD ["sh", "-c", "sudo service sshd start; bash"]
