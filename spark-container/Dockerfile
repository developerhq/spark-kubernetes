FROM java:openjdk-8-jdk

ENV hadoop_ver 2.8.2
ENV spark_ver 2.4.4

RUN mkdir -p /opt && \
    cd /opt && \
    curl http://archive.apache.org/dist/hadoop/common/hadoop-${hadoop_ver}/hadoop-${hadoop_ver}.tar.gz | \
        tar -zx && \
    ln -s hadoop-${hadoop_ver} hadoop && \
    echo Hadoop ${hadoop_ver} installed in /opt

RUN mkdir -p /opt && \
    cd /opt && \
    curl http://archive.apache.org/dist/spark/spark-${spark_ver}/spark-${spark_ver}-bin-without-hadoop.tgz | \
        tar -zx && \
    ln -s spark-${spark_ver}-bin-without-hadoop spark && \
    echo Spark ${spark_ver} installed in /opt

ENV SPARK_HOME=/opt/spark
ENV PATH=$PATH:$SPARK_HOME/bin
ENV HADOOP_HOME=/opt/hadoop
ENV PATH=$PATH:$HADOOP_HOME/bin
ENV LD_LIBRARY_PATH=$HADOOP_HOME/lib/native

RUN curl https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.8.2/hadoop-aws-2.8.2.jar -o /opt/spark/jars/hadoop-aws-2.8.2.jar
RUN curl https://repo1.maven.org/maven2/org/apache/httpcomponents/httpclient/4.5.3/httpclient-4.5.3.jar -o /opt/spark/jars/httpclient-4.5.3.jar
RUN curl https://repo1.maven.org/maven2/joda-time/joda-time/2.9.9/joda-time-2.9.9.jar -o /opt/spark/jars/joda-time-2.9.9.jar
RUN curl https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-core/1.11.712/aws-java-sdk-core-1.11.712.jar -o /opt/spark/jars/aws-java-sdk-core-1.11.712.jar
RUN curl https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk/1.11.712/aws-java-sdk-1.11.712.jar -o /opt/spark/jars/aws-java-sdk-1.11.712.jar
RUN curl https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-kms/1.11.712/aws-java-sdk-kms-1.11.712.jar -o /opt/spark/jars/aws-java-sdk-kms-1.11.712.jar
RUN curl https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-s3/1.11.712/aws-java-sdk-s3-1.11.712.jar -o /opt/spark/jars/aws-java-sdk-s3-1.11.712.jar

ADD start-common.sh start-worker start-master /
ADD core-site.xml /opt/spark/conf/core-site.xml
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf
ENV PATH $PATH:/opt/spark/bin
