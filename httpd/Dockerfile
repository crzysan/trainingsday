FROM ubi8
ENV DOCROOT=/var/www/html
LABEL maintainer="Chris <chris@dab.com>" \
      io.k8s.display-name="Apache HTTP Server" \
      io.openshift.expose-services="8080:http"

RUN yum install -y --nodocs --disableplugin=subscription-manager httpd && \
      yum clean all --disableplugin=subscription-manager -y && \
      echo "Hello I'm Batman!" > ${DOCROOT}/index.html && \ 
      sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf && \
      chgrp -R 0 /var/log/httpd /var/run/httpd && \
      chmod -R g=u /var/log/httpd /var/run/httpd

EXPOSE 8080
USER 1001
WORKDIR ${DOCROOT}
VOLUME ${DOCROOT}
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]
