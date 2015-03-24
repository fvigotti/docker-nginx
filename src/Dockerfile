FROM fvigotti/fatubuntu

# based on : https://github.com/nginxinc/docker-nginx/blob/master/Dockerfile


RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/debian/ wheezy nginx" >> /etc/apt/sources.list

ENV NGINX_VERSION 1.7.10-1~wheezy

RUN apt-get update && \
    apt-get install -y ca-certificates nginx=${NGINX_VERSION} && \
    rm -rf /var/lib/apt/lists/*

VOLUME ["/etc/nginx"]
VOLUME ["/var/cache/nginx"]
VOLUME ["/var/log/nginx/"]

# EXPOSE 80 443

ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]
