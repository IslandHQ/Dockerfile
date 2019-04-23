FROM mhart/alpine-node:latest
RUN mkdir /home/wt && cd /home/wt && npm i torrent-web --no-audit
ENTRYPOINT ["node","/home/wt/node_modules/torrent-web/"]
CMD ["-p=80"]
