FROM nginx:1.15.7-alpine

RUN sed -i "s/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g" /etc/apk/repositories

# apk update && install bash
RUN apk update \
        && apk upgrade \
        && apk add --no-cache bash bash-doc bash-completion \
        && rm -rf /var/cache/apk/* \
        && /bin/bash
COPY  ./sh/nginx.sh       /usr/bin

RUN  chmod  775  /usr/bin/nginx.sh

CMD [ "nginx"]

