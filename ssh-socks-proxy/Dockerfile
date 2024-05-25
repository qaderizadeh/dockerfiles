FROM alpine

RUN apk update && apk add openssh-client

ENV HOST=localhost
ENV PORT=22
ENV USER=root

CMD ssh -p $PORT -o StrictHostKeyChecking=no -D 0.0.0.0:1080 -q -C -N $USER@$HOST

# docker start <container_name> && \
# docker exec <container_name> mkdir -p /root/.ssh && \
# docker cp /path/to/id_rsa <container_name>:/root/.ssh/id_rsa && \
# docker cp /path/to/id_rsa.pub <container_name>:/root/.ssh/id_rsa.pub