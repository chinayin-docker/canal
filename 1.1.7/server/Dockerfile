#
#
#--------------------------------------------------------------------------
# canal-1.1.7
#--------------------------------------------------------------------------
#

FROM chinayin/openjdk:8-jre
LABEL maintainer="chinayin <whereismoney@qq.com>"

ENV CANAL_TYPE="server" CANAL_VERSION="1.1.7"
ENV CANAL_HOME /app/$CANAL_TYPE

COPY bin/ /app

RUN set -eux; \
    install_packages curl file net-tools; \
    \
    mkdir -p $CANAL_HOME; \
    \
    downloadUrl="https://github.com/alibaba/canal/releases/download/canal-$CANAL_VERSION/canal.deployer-$CANAL_VERSION.tar.gz"; \
    curl -fsSL -o canal.tgz "$downloadUrl"; \
    tar -xzvf canal.tgz --directory "$CANAL_HOME"; \
    rm canal.tgz*; \
    \
    rm -f $CANAL_HOME/bin/*.bat; \
    mv -f /app/*.sh "$CANAL_HOME/bin/"; \
    chmod +x $CANAL_HOME/bin/*.sh; \
    rm -rf $CANAL_HOME/conf/example; \
    \
    # fix bug: org.h2.jdbc.JdbcSQLDataException: Value too long for column "CHARACTER VARYING"
    curl -fsSL -o "$CANAL_HOME/lib/h2-2.2.224.jar" "https://repo1.maven.org/maven2/com/h2database/h2/2.2.224/h2-2.2.224.jar"; \
    rm -f $CANAL_HOME/lib/h2-2.1.210.jar; \
    \
    printf "canal=$CANAL_TYPE\n path=$CANAL_HOME"; \
    java -version

EXPOSE 11111

WORKDIR /app

CMD [ "./server/bin/startup.sh" ]
