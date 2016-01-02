FROM centos:latest

ENV JAVA_M_VERSION 8
ENV JAVA_VERSION 8u66
ENV BUILD_VERSION b17

ENV TOMCAT_M_VERSION 8
ENV TOMCAT_VERSION 8.0.30

RUN yum update -y && yum install -y curl \
				    vim  \
				    wget \
				    fuser
RUN wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/$JAVA_VERSION-$BUILD_VERSION/jdk-$JAVA_VERSION-linux-x64.rpm" -O /tmp/jdk-$JAVA_M_VERSION-linux-x64.rpm \
                  && yum -y install /tmp/jdk-$JAVA_M_VERSION-linux-x64.rpm && rm /tmp/jdk-$JAVA_M_VERSION-linux-x64.rpm \
		  && alternatives --install /usr/bin/java jar /usr/java/latest/bin/java 200000 \
		  && alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000 \ 
		  && alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000 \
		  && wget http://www.eu.apache.org/dist/tomcat/tomcat-$TOMCAT_M_VERSION/v${TOMCAT_VERSION}/bin/apache-tomcat-8.0.30.tar.gz -O /tmp/catalina.tar.gz \
		  && tar xzf /tmp/catalina.tar.gz -C /opt  \
		  && ln -s /opt/apache-tomcat-${TOMCAT_VERSION} /opt/tomcat \
		  && rm /tmp/catalina.tar.gz \		  
                  && rm -rf /opt/tomcat/webapps/examples /opt/tomcat/webapps/docs 
ENV CATALINA_HOME /opt/tomcat
ENV PATH $PATH:$CATALINA_HOME/bin
ENV JAVA_HOME /usr/java/latest
VOLUME ["/opt/tomcat/logs", "/opt/tomcat/work", "/opt/tomcat/temp", "/tmp/hsperfdata_root" ]
EXPOSE 8080 443
CMD ["catalina.sh", "run"]
