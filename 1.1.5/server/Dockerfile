#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#

FROM openjdk:8-jdk-slim
LABEL maintainer="chinayin <whereismoney@qq.com>" Version="v1.1.5-alpha-3"
ENV DEBIAN_FRONTEND=noninteractive DEPLOY_IMAGE_VERSION="2021-01-07 16:23"
ENV CANAL_TYPE="server" CANAL_VERSION="1.1.5-alpha-3"

ARG CHANGE_SOURCE=true
ARG TIMEZONE=Asia/Shanghai
RUN if [ $CHANGE_SOURCE = true ]; then \
    sed -i 's/deb.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list && \
    sed -i 's/security-cdn.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list \
;fi && cp /usr/share/zoneinfo/$TIMEZONE /etc/localtime && echo "$TIMEZONE" > /etc/timezone;

RUN set -eux; \
    apt-get update; \
    apt-get autoremove -y; \
    apt-get upgrade -y; \
    apt-get install -y --no-install-recommends \
        apt-utils wget vim procps iputils-ping telnet file \
    ; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*; \
    printf "alias ls='ls --color=auto'\nalias ll='ls -l --color=auto'\nalias l='ls -lA --color=auto'" >> /root/.bashrc

ADD files/canal.$CANAL_TYPE.tgz /app/$CANAL_TYPE
COPY bin/ /app

RUN set -eux; \
    export CANAL_PATH="/app/$CANAL_TYPE"; \
    \
    rm -f $CANAL_PATH/bin/*.bat; \
    mv -f /app/*.sh "$CANAL_PATH/bin/"; \
    chmod +x $CANAL_PATH/bin/*.sh; \
    rm -rf $CANAL_PATH/conf/example; \
    \
    printf "canal=$CANAL_TYPE\n path=$CANAL_PATH"; \
    java -version

EXPOSE 11111

WORKDIR /app

CMD [ "./server/bin/startup.sh" ]
