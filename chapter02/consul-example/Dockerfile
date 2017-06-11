FROM alpine:latest
LABEL maintainer="Russ McKendrick <russ@mckendrick.io>"
LABEL description="An image with the latest version on Consul."

ENV CONSUL_VERSION 0.8.4
ENV CONSUL_SHA256 c8859a0a34c50115cdff147f998b2b63226f5f052e50f342209142420d1c2668
ENV CONSUL_UI_SHA256 7a49924a872205002b2bf72af8c82d5560d4a7f4a58b2f65ee284dd254ebd063

RUN  apk add --update ca-certificates wget && \
     wget -O consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip && \
     echo "$CONSUL_SHA256 *consul.zip" | sha256sum -c - && \
     unzip consul.zip && \
     mv consul /bin/ && \
     rm -rf consul.zip && \
     cd /tmp && \
     wget -O ui.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_web_ui.zip && \
     echo "$CONSUL_UI_SHA256 *ui.zip" | sha256sum -c - && \
     unzip ui.zip && \
     mkdir -p /ui && \
     mv * /ui && \
     rm -rf /tmp/* /var/cache/apk/*

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp

VOLUME [ "/data" ]

ENTRYPOINT [ "/bin/consul" ]
CMD [ "agent", "-data-dir", "/data", "-server", "-bootstrap-expect", "1", "-ui-dir", "/ui", "-client=0.0.0.0"]