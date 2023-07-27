FROM ubuntu
RUN apt-get update && apt-get -y upgrade
RUN apt-get install -y curl && apt-get install -y jq

RUN curl -OL https://github.com/elkowar/pipr/releases/download/v0.0.16/pipr
RUN chmod +x ./pipr
RUN mv ./pipr /usr/local/bin
WORKDIR /var/pipr

RUN apt-get install bubblewrap
