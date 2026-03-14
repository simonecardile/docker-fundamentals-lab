FROM alpine:3.20

RUN apk add --no-cache bash curl bind-tools

WORKDIR /workspace

COPY scripts/welcome.sh /usr/local/bin/welcome.sh
RUN chmod +x /usr/local/bin/welcome.sh

CMD ["sh", "-c", "welcome.sh && tail -f /dev/null"]
