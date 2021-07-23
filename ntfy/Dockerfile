FROM alpine:latest as builder
LABEL mainainer='b3vis'
RUN apk upgrade --no-cache \
    && apk add --no-cache \
    alpine-sdk \
    python3-dev \
    py3-pip \
    openssl-dev \
    libffi-dev \
    git \
    && pip3 install --upgrade pip 

RUN git clone https://github.com/dschep/ntfy.git \
    && cd ntfy \
    && pip3 install --upgrade ntfy[pid,emoji,xmpp,telegram,instapush,slack,rocketchat,slack_webhook]

# FROM b3vis/borgmatic:v1.1.16-1.5.14
FROM b3vis/borgmatic:latest
LABEL mainainer='b3vis'
VOLUME /root/.config/ntfy
COPY --from=builder /usr/lib/python3.9/site-packages /usr/lib/python3.9/
COPY --from=builder /usr/bin/ntfy /usr/bin/
