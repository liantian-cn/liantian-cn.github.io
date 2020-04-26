FROM alpine:latest


RUN  sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
&&  apk update \
&&  apk upgrade \ 
&& apk add --no-cache smokeping lighttpd ttf-opensans supervisor \
&& rm -rf /var/cache/apk/* \
&& rm -rf /var/www/localhost/htdocs/ \
&& ln -s /usr/share/webapps/smokeping /var/www/localhost/htdocs \
&& chmod 777 /var/lib/smokeping/.simg \
&& chmod u+s /usr/sbin/fping \
&& chmod 777 /var/log/lighttpd \
&& rm -f /etc/lighttpd/lighttpd.conf




COPY lighttpd.conf /etc/lighttpd/
COPY supervisord.conf /etc/supervisord.conf
CMD ["/usr/bin/supervisord"]



VOLUME /config

EXPOSE 32080