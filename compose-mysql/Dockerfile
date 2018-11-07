FROM ubuntu:18.04
LABEL maintainer="Sidney Coelho <sidney.coelho@najjah.33mail.com>"

RUN apt-get update && \
    apt-get -y install \
    nginx \
    unzip \
    wget \
    ca-certificates \
    php7.2 php7.2-fpm php7.2-cli php7.2-json php7.2-curl php7.2-xml php7.2-zip && \
    mkdir /pagekit
ADD ../nginx/nginx.conf /etc/nginx/nginx.conf

WORKDIR /pagekit
VOLUME ["/pagekit/storage", "/pagekit/app/cache"]
ENV PAGEKIT_VERSION 1.0.14

RUN wget https://github.com/pagekit/pagekit/releases/download/$PAGEKIT_VERSION/pagekit-$PAGEKIT_VERSION.zip -O /pagekit/pagekit.zip && \
    unzip /pagekit/pagekit.zip && \
    rm /pagekit/pagekit.zip && \
    chown -R www-data: /pagekit

RUN apt-get autoremove wget unzip -y && \
    apt-get autoclean -y && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["sh", "-c", "chown -R www-data: /pagekit && service php7.2-fpm start && nginx"]
