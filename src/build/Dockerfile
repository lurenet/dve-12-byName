FROM ubuntu:20.04

ENV TZ=Europe/Kiev
ENV WARDIR=/tmp/webapps/war
ENV CONFDIR=/tmp/webapps/conf

# DB
ENV DBCONF=WebContent/Config.properties
ENV DBNAME=app42
ENV DBUSER=tomcat
ENV DBPASSWD=yJebq3iVChtH49UU
ENV DBIP=10.0.0.2
ENV DBPORT=3306

RUN ln -snf /usr/share/zoneinfo/$TZ etc/localtime && echo $TZ > /etc/timezone
RUN apt update && apt install maven git -y

WORKDIR tmp
RUN git clone https://github.com/shephertz/App42PaaS-Java-MySQL-Sample.git

WORKDIR App42PaaS-Java-MySQL-Sample
RUN find "$DBCONF" -exec sed -i -e "s/$(grep app42.paas.db.name $DBCONF)/app42.paas.db.name = "$DBNAME"/" "{}" \; && \
    find "$DBCONF" -exec sed -i -e "s/$(grep app42.paas.db.username $DBCONF)/app42.paas.db.username = "$DBUSER"/" "{}" \; && \
    find "$DBCONF" -exec sed -i -e "s/$(grep app42.paas.db.password $DBCONF)/app42.paas.db.password = "$DBPASSWD"/" "{}" \; && \
    find "$DBCONF" -exec sed -i -e "s/$(grep app42.paas.db.ip $DBCONF)/app42.paas.db.ip = "$DBIP"/" "{}" \; && \
    find "$DBCONF" -exec sed -i -e "s/$(grep app42.paas.db.port $DBCONF)/app42.paas.db.port = "$DBPORT"/" "{}" \;

RUN mvn clean && mvn install
RUN mkdir -p $WARDIR && cp target/App42PaaS-Java-MySQL-Sample-0.0.1-SNAPSHOT.war $WARDIR/app42.war
RUN mkdir -p $CONFDIR && cp $DBCONF $CONFDIR/
