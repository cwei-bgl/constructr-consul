# FROM frolvlad/alpine-oraclejdk8
FROM consul:1.0.0

# Copy the built distro into the Container
COPY target/universal/*.tgz /mnt/package.tgz
COPY docker/supervisord.conf /etc/supervisord.conf
RUN mkdir -p /opt/supervisor \
  && mkdir -p /opt/constructr-coordination-demo/logs \
  && mkdir -p /opt/consul/logs \
  && adduser -S constructr_consul_demo

ENV JAVA_ALPINE_VERSION 8.131.11-r2
RUN apk update \
  && apk add bash \
    openjdk8-jre="$JAVA_ALPINE_VERSION" \
    supervisor \
    tar
RUN tar zxvf /mnt/package.tgz --strip-components=1 -C /mnt

# Open up the application port
EXPOSE 8000
# Open up the JMX port
EXPOSE 9010

# USER constructr_consul_demo
WORKDIR /mnt
ENTRYPOINT [ "/usr/bin/supervisord", "-n", "-c", "/etc/supervisord.conf" ]
# ENTRYPOINT ["/bin/sh"]
