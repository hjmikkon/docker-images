FROM centos:centos7

MAINTAINER John Gasper <jtgasper3@gmail.com>

RUN yum -y update \
    && yum -y install wget \
    && wget http://download.opensuse.org/repositories/security://shibboleth/CentOS_7/security:shibboleth.repo -P /etc/yum.repos.d \
    && yum -y install httpd shibboleth.x86_64 \
    && yum -y clean all

RUN test -d /var/run/lock || mkdir -p /var/run/lock \
    && test -d /var/lock/subsys/ || mkdir -p /var/lock/subsys/ \
    && chmod +x /etc/shibboleth/shibd-redhat \
    && echo $'export LD_LIBRARY_PATH=/opt/shibboleth/lib64:$LD_LIBRARY_PATH\n'\
       > /etc/sysconfig/shibd \
    && chmod +x /etc/sysconfig/shibd
    
RUN chown -R shibd:root /var/run/shibboleth
RUN chmod -R 777 /var/run/shibboleth
RUN chmod -R 777 /run/httpd

COPY httpd-shibd-foreground /usr/local/bin/

EXPOSE 8443 8080

CMD ["httpd-shibd-foreground"]
