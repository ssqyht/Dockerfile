FROM node:11-alpine as builder

COPY repositories /etc/apk/repositories
RUN apk update && apk add --no-cache  git python make openssl tar gcc
#ADD yapi.tgz /home/

RUN wget -O yapi.tgz http://registry.npm.taobao.org/yapi-vendor/download/yapi-vendor-1.7.0.tgz
RUN tar zxvf yapi.tgz -C /home
RUN mkdir /api && mv /home/package /api/vendors
RUN cd /api/vendors && \
    npm install --production --registry https://registry.npm.taobao.org

FROM node:11-alpine

MAINTAINER JackYuan
ENV TZ="Asia/Shanghai" HOME="/"
WORKDIR ${HOME}

COPY --from=builder /api/vendors /api/vendors
COPY config.json /api/config.json
EXPOSE 3000

COPY docker-entrypoint.sh /api/docker-entrypoint.sh
COPY docker-entryenv.sh /api/docker-entryenv.sh

RUN chmod 755 /api/docker-entrypoint.sh
RUN chmod 755 /api/docker-entryenv.sh

ENTRYPOINT ["/api/docker-entrypoint.sh"]




