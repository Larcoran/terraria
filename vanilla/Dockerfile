FROM alpine:3.11.6 AS base

RUN apk add --update-cache \
    unzip

ENV DL_LINK=https://terraria.org/system/dedicated_servers/archives/000/000/039/original/terraria-server-1405.zip
ENV DL_VERSION=1405
ENV DL_FILE=terraria-server.zip

ADD $DL_LINK /$DL_FILE

RUN unzip /$DL_FILE -d /terraria && \
    mkdir /terraria-server && \
    mv /terraria/$DL_VERSION/Linux/* /terraria-server && \
    chmod +x /terraria-server/TerrariaServer && \
    chmod +x /terraria-server/TerrariaServer.bin.x86_64

FROM mono:6.8.0.96-slim
LABEL maintainer="Ryan Sheehan <rsheehan@gmail.com>"

EXPOSE 7777

VOLUME ["/root/.local/share/Terraria/Worlds", "/config"]

COPY --from=base /terraria-server/ /terraria-server/

ENTRYPOINT ["/terraria-server/TerrariaServer"]
