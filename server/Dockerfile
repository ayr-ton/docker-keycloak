FROM jboss/base-jdk:7

ENV KEYCLOAK_VERSION 1.3.1.Final

USER root

RUN yum install -y epel-release && yum install -y jq && yum clean all

USER jboss

RUN cd /opt/jboss/ && curl http://central.maven.org/maven2/org/keycloak/keycloak-server-dist/$KEYCLOAK_VERSION/keycloak-server-dist-$KEYCLOAK_VERSION.tar.gz | tar zx && mv /opt/jboss//keycloak-$KEYCLOAK_VERSION /opt/jboss/keycloak

ADD setLogLevel.xsl /opt/jboss/keycloak/
RUN java -jar /usr/share/java/saxon.jar -s:/opt/jboss/keycloak/standalone/configuration/standalone.xml -xsl:/opt/jboss/keycloak/setLogLevel.xsl -o:/opt/jboss/keycloak/standalone/configuration/standalone.xml

ENV JBOSS_HOME /opt/jboss/keycloak

EXPOSE 8080

CMD ["/opt/jboss/keycloak/bin/standalone.sh", "-b", "0.0.0.0"]
