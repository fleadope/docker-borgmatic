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
    && pip3 install --upgrade pip wheel


RUN git clone https://github.com/dschep/ntfy.git \
    && cd ntfy \
    && PYTHONUSERBASE=/tmp pip3 install --user --force-reinstall .

FROM b3vis/borgmatic:latest
LABEL mainainer='b3vis'
VOLUME /root/.config/ntfy

COPY --from=builder /tmp/lib/python3.9/site-packages /usr/lib/python3.8
COPY --from=builder /tmp/bin /usr/bin/
