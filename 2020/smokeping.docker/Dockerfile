FROM alpine:latest


RUN  sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
&&  apk update \
&&  apk upgrade \ 
&& apk add --no-cache smokeping lighttpd ttf-opensans supervisor bind-tools gawk tcptraceroute  \
&& rm -rf /var/cache/apk/* \
&& rm -rf /var/www/localhost/htdocs/ \
&& ln -s /usr/share/webapps/smokeping /var/www/localhost/htdocs \
&& chmod 777 /var/lib/smokeping/.simg \
&& chmod u+s /usr/sbin/fping \
&& chmod 777 /var/log/lighttpd \
&& rm -f /etc/lighttpd/lighttpd.conf \
&& rm -f /etc/smokeping/config





COPY lighttpd.conf /etc/lighttpd/
COPY supervisord.conf /etc/supervisord.conf
COPY tcpping /usr/bin/
RUN chmod +x /usr/bin/tcpping

CMD ["/usr/bin/supervisord"]



VOLUME /etc/smokeping/config

EXPOSE 32080