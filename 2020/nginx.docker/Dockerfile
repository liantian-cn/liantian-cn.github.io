FROM alpine:latest

RUN  sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
&&  apk update \
&&  apk upgrade \ 
&&  apk add --no-cache nginx \
&&  rm -rf /var/cache/apk/*   \
&& ln -sf /dev/stdout /var/log/nginx/access.log \
&& ln -sf /dev/stderr /var/log/nginx/error.log \
&& rm -f /etc/nginx/conf.d/default.conf \
&& mkdir -p /config/  \
&& mkdir -p /wwwroot/ \
&& mkdir -p /run/nginx \
&& sed -i 's|include /etc/nginx/conf.d/\*.conf;| include /config/nginx/conf.d/\*.conf;|g' /etc/nginx/nginx.conf


STOPSIGNAL SIGTERM

EXPOSE 80

VOLUME ["/config", "/wwwroot"]
CMD ["nginx", "-g", "daemon off;"]
