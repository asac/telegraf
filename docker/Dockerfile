FROM golang:alpine as builder

RUN apk update; apk add git make

WORKDIR /work
ADD . .

RUN GOOS=linux GOARCH=arm GOARM=5 make -j

FROM arm32v6/alpine

COPY qemu-arm-static /usr/bin/

ADD etc /etc/telegraf

COPY --from=builder /work/telegraf /bin/telegraf

RUN apk add ca-certificates; rm -rf /var/cache/apk/*

CMD [ "telegraf" ]

