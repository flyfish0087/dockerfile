FROM python:3.6-alpine3.6
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories && apk update

ENV GIT_BRANCH=bdf506a55596db4495b2baf91fba4088bb64fdc2
RUN set -xe \
 && apk add --no-cache git \
 && git clone -b dev --depth 5 https://github.com/jumpserver/jumpserver /app/jumpserver \
 && cd /app/jumpserver \
 && [ "$GIT_BRANCH" == $(git rev-parse HEAD) ] || git checkout $GIT_BRANCH \
 && rm -rf .git \
 && apk del git

WORKDIR /app/jumpserver

RUN set -xe \
    && apk add --no-cache \
    sudo bash openssh-client sshpass sqlite-dev zlib-dev libressl-dev jpeg-dev freetype-dev lcms2-dev libwebp-dev \
    python3-dev linux-headers libffi-dev mariadb-dev libgsasl-dev openldap-dev krb5-dev

RUN set -xe \
 && apk add --no-cache --virtual .build-deps build-base \
 && pip install -i https://mirrors.aliyun.com/pypi/simple/ -r requirements/requirements.txt \
 && apk del .build-deps

ADD config.py run_server.py ./
EXPOSE 8080

CMD [ "python", "-u", "run_server.py", "all" ]