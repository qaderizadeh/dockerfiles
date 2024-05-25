FROM alpine

RUN apk update && apk add v2ray

CMD echo $CONFIG | v2ray run -format json