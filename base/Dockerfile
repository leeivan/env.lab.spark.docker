FROM openjdk:8u212-b04-jdk-stretch
LABEL author="Ivan Lee" email="leeivan2008@gmail.com"
LABEL version="1.0"

ENV DAEMON_RUN=true
ENV SPARK_VERSION=2.4.5
ENV HADOOP_VERSION=2.7
ENV SCALA_VERSION=2.12.4
ENV SCALA_HOME=/usr/share/scala
ENV SPARK_HOME=/spark
ENV PATH="/usr/local/sbt/bin:/spark/bin:${PATH}"

RUN apt-get update && apt-get install -y curl vim wget software-properties-common ssh net-tools ca-certificates jq netcat telnet nano

WORKDIR /root
ADD . /root

# Install scala
RUN mkdir "${SCALA_HOME}"
RUN tar xzf *scala* --strip-components 1 -C "${SCALA_HOME}"
RUN ln -s "${SCALA_HOME}/bin/"* "/usr/bin/"

RUN  mkdir /data
RUN  mv ./data/* /data/

# Installing sbt
RUN mkdir -p /usr/local/sbt
RUN tar xzf *sbt* --strip-components 1 -C /usr/local/sbt
RUN sbt sbtVersion

# Installing Spark
RUN mkdir -p "${SPARK_HOME}"
RUN tar xzf *spark* --strip-components 1 -C "${SPARK_HOME}"

# Installing Maven.
RUN mkdir -p /usr/local/apache-maven
RUN tar xzf *maven* --strip-components 1 -C /usr/local/apache-maven
ENV MAVEN_HOME /usr/local/apache-maven
ENV PATH="/usr/local/apache-maven/bin:${PATH}"

# Installing HBase
RUN mkdir -p /usr/local/hbase
RUN tar xzf hbase* --strip-components 1 -C /usr/local/hbase
ENV HBASE_HOME /usr/local/hbase
ENV PATH="/usr/local/hbase/bin::${PATH}"

# Add Dependencies for PySpark
RUN apt-get install -y python3 python3-pip python3-numpy python3-matplotlib python3-scipy python3-pandas python3-simpy
RUN update-alternatives --install "/usr/bin/python" "python" "$(which python3)" 1

RUN rm -rf /root/*
