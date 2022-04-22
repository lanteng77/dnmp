FROM scratch
ADD centos-7-x86_64-docker.tar.xz /
LABEL maintainer="lanteng77@gmail.com"

ADD nginx-1.19.7.tar.gz /usr/local/
RUN groupadd -g 1001 nginx && useradd -g nginx -u 1001 -s /sbin/nologin nginx && cd /usr/local/nginx-1.19.7 && ./configure --prefix=/usr/local/nginx --user=nginx --group=nginx --with-http_ssl_module --with-stream && make && make install && ln -sv /usr/local/nginx/sbin/nginx /usr/bin && rm -rf /usr/local/nginx-1.19.7 && rm -rf /usr/local/nginx-1.19.7.tar.gz
ADD nginx.conf /usr/local/nginx/conf/nginx.conf
ADD mycsdn.html /nginx/index.html

RUN chown -R nginx:nginx /usr/local/nginx /nginx

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
