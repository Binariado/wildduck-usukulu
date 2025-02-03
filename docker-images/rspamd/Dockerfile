
FROM alpine:3

ARG version=3.10.2

RUN apk add --no-cache tini

RUN apk add --no-cache \
    rspamd=${version}-r1 \
    rspamd-controller=${version}-r1 \
    rspamd-proxy=${version}-r1 \
    rspamd-fuzzy=${version}-r1 ca-certificates curl

EXPOSE 11332/tcp 11333/tcp 11334/tcp

ENTRYPOINT ["/sbin/tini", "--", "/usr/sbin/rspamd"]
CMD ["-i", "-f"]