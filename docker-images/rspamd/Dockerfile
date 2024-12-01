
FROM alpine:3

ARG version=3.8.4

RUN apk add --no-cache tini

RUN apk add --no-cache \
    rspamd=${version}-r0 \
    rspamd-controller=${version}-r0 \
    rspamd-proxy=${version}-r0 \
    rspamd-fuzzy=${version}-r0 ca-certificates curl

EXPOSE 11332/tcp 11333/tcp 11334/tcp

ENTRYPOINT ["/sbin/tini", "--", "/usr/sbin/rspamd"]
CMD ["-i", "-f"]