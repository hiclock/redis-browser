FROM ruby:2.3.1-alpine

MAINTAINER zhouyq <zhouyq@goodrain.com>


# timezone
RUN apk add --no-cache tzdata libc6-compat && \
       ln -s /lib /lib64 && \
       cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
       echo "Asia/Shanghai" >  /etc/timezone && \
       date && apk del --no-cache tzdata
       
# add bash and git
RUN apk add --no-cache bash git nodejs && \
    sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

RUN mkdir /opt/ && \
    cd /opt && \
    git clone https://github.com/monterail/redis-browser.git && \
    cd redis-browser && \
    gem install redis-browser

RUN apk add --no-cache wget curl netcat-openbsd && apk del --no-cache git tzdata

ADD docker-entrypoint.sh /usr/bin/

RUN chmod +x /usr/bin/docker-entrypoint.sh 


EXPOSE 4567

ENTRYPOINT ["docker-entrypoint.sh"]
