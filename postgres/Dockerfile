FROM postgres:13
LABEL Description="Esta imagen sirve para la configuración de la capa de base de datos" Version="1.0"

ARG locale=es_CL
ARG MY_TZ=America/Santiago

ENV LANG ${locale}.utf8
ENV WEB_MY_TZ=${MY_TZ}

# Locale
RUN localedef -i ${locale} -c -f UTF-8 -A /usr/share/locale/locale.alias ${locale}.UTF-8

# TZ
RUN echo "${WEB_MY_TZ}" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update && \
    apt-get install -y dos2unix

COPY conf/restore_dump.sh /docker-entrypoint-initdb.d/restore_dump.sh

RUN dos2unix /docker-entrypoint-initdb.d/restore_dump.sh

RUN chmod -R +x /docker-entrypoint-initdb.d/restore_dump.sh
