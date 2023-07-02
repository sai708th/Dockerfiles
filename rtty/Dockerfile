FROM golang:1.20

WORKDIR /usr/src/app

RUN apt update && \
    apt-get update 

RUN apt install -y tree zsh 

RUN apt install -y locales && \
    locale-gen ja_JP.UTF-8

RUN go install github.com/skanehira/rtty@latest

CMD zsh
