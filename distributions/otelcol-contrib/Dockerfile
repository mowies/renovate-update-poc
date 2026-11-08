FROM alpine:3.24@sha256:3f4d6b32e26703c6082839234f43769d5046b3ac7c910033911d1e71d8cd630a as certs
RUN apk --update add ca-certificates

FROM scratch

ARG USER_UID=10001
ARG USER_GID=10001
USER ${USER_UID}:${USER_GID}

COPY --from=certs /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --chmod=755 otelcol-contrib /otelcol-contrib
COPY config.yaml /etc/otelcol-contrib/config.yaml
ENTRYPOINT ["/otelcol-contrib"]
CMD ["--config", "/etc/otelcol-contrib/config.yaml"]
EXPOSE 4317 4318 55679
