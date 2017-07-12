FROM centos:centos7
MAINTAINER jtoledog <jptgjuanpablo@gmail.com>

RUN yum -y update; yum clean all
RUN yum -y install openssh-server passwd openssh-clients; yum clean all
ADD ./start.sh /start.sh
RUN mkdir /var/run/sshd


RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' 

RUN chmod 755 /start.sh
EXPOSE 22
RUN ./start.sh


# Java Install
ENV JAVA_VERSION 8u131
ENV BUILD_VERSION b11
ADD jdk-8u131-linux-x64.rpm /tmp/
RUN yum -y install /tmp/jdk-8u131-linux-x64.rpm
RUN alternatives --install /usr/bin/java jar /usr/java/latest/bin/java 200000
RUN alternatives --install /usr/bin/javaws javaws /usr/java/latest/bin/javaws 200000
RUN alternatives --install /usr/bin/javac javac /usr/java/latest/bin/javac 200000
ENV JAVA_HOME /usr/java/latest

# Install Tomcat RPM
RUN yum -y install tomcat tomcat-webapps tomcat-admin-webapps
ADD tomcat.conf /etc/tomcat/tomcat.conf
ADD jenkins.war /var/lib/tomcat/webapps/
EXPOSE 8080/tcp
EXPOSE 50000/tcp

CMD ["/usr/libexec/tomcat/server", "start"]