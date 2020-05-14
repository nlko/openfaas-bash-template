FROM openfaas/classic-watchdog:0.18.1 as watchdog

FROM alpine:3.11
RUN apk --no-cache add ca-certificates \
    && addgroup -S app && adduser -S -g app app \
    && mkdir -p /home/app \
    && chown app /home/app

WORKDIR /home/app

COPY --from=watchdog /fwatchdog .
COPY function/handler.sh    .

RUN chown -R app /home/app

USER app

ENV fprocess="/home/app/handler.sh"
EXPOSE 8080

HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

CMD ["./fwatchdog"]
