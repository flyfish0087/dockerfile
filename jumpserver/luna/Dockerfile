FROM alpine
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories \
 && apk add --update --no-cache curl \
 && mkdir /data && cd /data \
 && curl -L https://github.com/jumpserver/luna/releases/download/0.5-beta-2/luna.tar.gz | tar -zx

VOLUME [ "/app/luna" ]

ENTRYPOINT [ "sh", "-c" ]
CMD [ "cp -r /data/luna /app && cat" ]