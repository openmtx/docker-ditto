FROM denoland/deno:2.1.1

ARG DITTO_REPO=https://gitlab.com/soapbox-pub/ditto.git

ARG PORT=4036

ENV PORT=${PORT}

USER root

RUN apt-get update \
&&  apt-get install -y zip unzip gzip curl git \
&&  apt-get clean \
&&  rm -rf /var/lib/apt/lists/* \
&&  mkdir /app \
&&  chown -R deno /app

COPY ./bin/* /usr/local/bin

WORKDIR /app

USER deno

RUN git clone ${DITTO_REPO} . \
&&  deno cache --allow-import src/server.ts || true \
&&  deno task soapbox

EXPOSE ${PORT}

ENTRYPOINT ["ditto-entrypoint.sh"]
