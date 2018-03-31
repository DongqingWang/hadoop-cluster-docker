# hadoop-cluster-docker: v1.0.0
Initial version contains only dockerfile of:

  1. hadoop-base
  2. hadoop
  3. hbase
  
To build the dockerfiles, should:

  1. In root directory: docker build -t dongqing/hadoop-base:1.0.0 .
  2. cd Hadoop: docker build -t dongqing/hadoop:1.0.0 .
  3. cd HBase: docker build -t dongqing/hbase:1.0.0 .
  
Containers to start:

  1. Hadoopmaster: docker run -itd --network docker_default --name hadoopmaster -h hadoopmaster -p 50070:50070 -p 8088:8088 dongqing/hadoop:1.0.0
  2. Hadoopstandby:  docker run -it --network docker_default --name hadoopstandby -h hadoopstandby dongqing/hadoop:1.0.0
  3. Hadoopslave1:  docker run -itd --network docker_default --name hadoopslave1 -h hadoopslave1 dongqing/hadoop:1.0.0
  4. Hadoopslave2:  docker run -itd --network docker_default --name hadoopslave2 -h hadoopslave2 dongqing/hadoop:1.0.0
  
  5. Hmaster: docker run -itd --network docker_default --name hmaster -h hmaster -p 16010:16010 dongqing/hbase:1.0.0
  6. Hregionserver1: docker run -itd --network docker_default --name hregionserver1 -h hregionserver1 dongqing/hbase:1.0.0
  7. Hregionserver2: docker run -itd --network docker_default --name hregionserver2 -h hregionserver2 dongqing/hbase:1.0.0
  
Steps to start hadoop and hbase:

  1. docker exec -it hadoopmaster bash
     - /usr/local/hadoop/sbin/start-dfs.sh
     - /usr/local/hadoop/sbin/start-yarn.sh
  2. docker exec -it hmaster bash
     - start-hbase.sh

Caveat:
  1. Hbase shutdown with error: Timedout 300000ms waiting for namespace table to be assigned
     - Solution: hbase org.apache.hadoop.hbase.util.hbck.OfflineMetaRepair
