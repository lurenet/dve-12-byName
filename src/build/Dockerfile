FROM ubuntu:20.04

ENV TZ=Europe/Kiev
ENV WARDIR=/tmp/webapps/war

RUN ln -snf /usr/share/zoneinfo/$TZ etc/localtime && echo $TZ > /etc/timezone
RUN apt update && apt install maven git -y

WORKDIR tmp
RUN git clone https://github.com/shephertz/App42PaaS-Java-MySQL-Sample.git

WORKDIR App42PaaS-Java-MySQL-Sample

RUN mvn clean && mvn install
RUN mkdir -p $WARDIR && cp target/App42PaaS-Java-MySQL-Sample-0.0.1-SNAPSHOT.war $WARDIR/
