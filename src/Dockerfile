FROM fvigotti/fatubuntu

# based on : https://github.com/nginxinc/docker-nginx/blob/master/Dockerfile
ENV NGINX_UBUNTU_DIST trusty
ENV NGINX_UBUNTU_ARCHITECTURE amd64

RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/ubuntu/ ${NGINX_UBUNTU_DIST} nginx" >> /etc/apt/sources.list

RUN export NGINX_VERSION=$(curl --silent "http://nginx.org/packages/mainline/ubuntu/dists/${NGINX_UBUNTU_DIST}/nginx/binary-${NGINX_UBUNTU_ARCHITECTURE}/Packages" |  grep -A 1 -e 'Package: nginx$' | grep -e  '^Version:' | sed 's/^Version: //') && \
    echo "NGINX_VERSION=${NGINX_VERSION}" && apt-get update && apt-get upgrade -y  && \
    apt-get install -y ca-certificates nginx=${NGINX_VERSION} && \
    rm -rf /var/lib/apt/lists/*


VOLUME ["/etc/nginx"]
VOLUME ["/var/cache/nginx"]
VOLUME ["/var/log/nginx/"]

# EXPOSE 80 443

ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]
