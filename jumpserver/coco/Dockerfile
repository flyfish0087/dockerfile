FROM python:3.6-alpine3.6
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories && apk update

ENV GIT_BRANCH=3319818f9cd81f1361bf3bc3fc30a13d09b1e389
RUN set -xe \
 && apk add --no-cache git \
 && git clone -b dev --depth 5 https://github.com/jumpserver/coco /app/coco \
 && cd /app/coco \
 && [ "$GIT_BRANCH" == $(git rev-parse HEAD) ] || git checkout $GIT_BRANCH \
 && rm -rf .git \
 && apk del git

WORKDIR /app/coco

RUN set -xe \
 && apk add --no-cache libffi-dev krb5-dev libressl-dev linux-headers \
 && apk add --no-cache --virtual .build-deps build-base  \
 && pip install -i https://mirrors.aliyun.com/pypi/simple/ -r requirements/requirements.txt \
 && apk del .build-deps

ADD conf.py ./
EXPOSE 5000 2222

CMD [ "python", "run_server.py" ]