FROM mhart/alpine-node:latest
RUN mkdir /home/wt 
WORKDIR /home/wt
RUN npm i torrent-web --no-audit
EXPOSE 80
ENTRYPOINT ["node","./node_modules/torrent-web/"]
