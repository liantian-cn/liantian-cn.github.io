FROM alpine:latest

ENV TZ=Asia/Shanghai
COPY ./qbittorrent /

RUN  sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories \
&&  apk update \
&&  apk upgrade \ 
&&  apk add --no-cache ca-certificates tzdata python3 bash nano openssl \
&&  rm -rf /var/cache/apk/*   \
&&  chmod a+x  /usr/local/bin/qbittorrent-nox   \
&&  mkdir -p ~/.config/qBittorrent/ssl \
&&  cd ~/.config/qBittorrent/ssl  \
&&  openssl req -new -newkey rsa:4096 -x509 -nodes -days 7300 -subj "/C=CC/ST=ST/L=LL/O=Dis/CN=qbittorrent.home.local" -out server.crt -keyout server.key  \
&&  echo "[Preferences]" >> /root/.config/qBittorrent/qBittorrent.conf \
&&  echo "Bittorrent\AutoUpdateTrackers=true" >> /root/.config/qBittorrent/qBittorrent.conf \
&&  echo "Bittorrent\CustomizeTrackersListUrl=https://trackerslist.com/all.txt" >> /root/.config/qBittorrent/qBittorrent.conf \
&&  echo "WebUI\Port=8080" >> /root/.config/qBittorrent/qBittorrent.conf \
&&  echo "WebUI\HTTPS\CertificatePath=/root/.config/qBittorrent/ssl/server.crt" >> /root/.config/qBittorrent/qBittorrent.conf \
&&  echo "WebUI\HTTPS\KeyPath=/root/.config/qBittorrent/ssl/server.key" >> /root/.config/qBittorrent/qBittorrent.conf \
&&  echo "WebUI\HTTPS\Enabled=false" >> /root/.config/qBittorrent/qBittorrent.conf 


VOLUME /DATA

EXPOSE 8080 8443 9068  9068/udp


CMD [ "/usr/local/bin/qbittorrent-nox" ]