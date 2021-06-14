ARG ELK_VERSION

FROM docker.elastic.co/beats/heartbeat:${ELK_VERSION}

COPY heartbeat.yml /usr/share/heartbeat/heartbeat.yml

USER root

RUN chown root:heartbeat /usr/share/heartbeat/heartbeat.yml

USER heartbeat