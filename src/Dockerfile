FROM quay.io/fravi/docker-fatubuntu1804:master

# based on : https://github.com/nginxinc/docker-nginx/blob/master/Dockerfile
ENV NGINX_UBUNTU_DIST bionic
ENV NGINX_UBUNTU_ARCHITECTURE amd64
ENV NGINX_VERSION 1.14.1-1~bionic

WORKDIR /root
RUN wget http://nginx.org/keys/nginx_signing.key && \
    apt-key add nginx_signing.key && \
    echo "deb http://nginx.org/packages/ubuntu/ bionic nginx" >> /etc/apt/sources.list && \
    echo "deb-src http://nginx.org/packages/ubuntu/ bionic nginx" >> /etc/apt/sources.list && \
    apt-get update &&  apt-get install -qy nginx=$NGINX_VERSION

#apt-cache policy nginx


#
#RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
#RUN echo "deb http://nginx.org/packages/mainline/ubuntu/ ${NGINX_UBUNTU_DIST} nginx" >> /etc/apt/sources.list
#
#RUN export NGINX_VERSION=$(curl --silent "http://nginx.org/packages/mainline/ubuntu/dists/${NGINX_UBUNTU_DIST}/nginx/binary-${NGINX_UBUNTU_ARCHITECTURE}/Packages" |  grep -A 1 -e 'Package: nginx$' | grep -e  '^Version:' | sed 's/^Version: //') && \
#    echo "NGINX_VERSION=${NGINX_VERSION}" && apt-get update && apt-get upgrade -y  && \
#    apt-get install -y ca-certificates nginx=${NGINX_VERSION} && \
#    rm -rf /var/lib/apt/lists/*

# delete conf.d/default.conf && prepare base dirs structure
RUN rm -rf /etc/nginx/*.d && \
	mkdir -p /etc/nginx/addon.d /etc/nginx/conf.d /etc/nginx/host.d /etc/nginx/nginx.d

# add /etc/nginx configuration, but do not overwrite existing default nginx configuration (Exception for /etc/nginx/nginx.conf )
ADD etc /etc

VOLUME ["/etc/nginx"]

# datafiles in : /data/http/
# logs in : /data/logs/
# plugin conf in : /data/config/nginx-*.conf
VOLUME ["/data"]

VOLUME ["/var/cache/nginx"]
VOLUME ["/var/log/nginx/"]

# EXPOSE 80 443

ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]
