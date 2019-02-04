FROM nginx

# Posible Channels: 
# ALPHA,BETA,SNAPSHOT,RELEASE
ENV CHANNEL BETA

RUN apt update -y && apt install curl unzip jq -y

# Parse,Download and Unzip the files

RUN \
export FILENAME=$(curl -s "https://api.madfix.me/v1/download.php?BRANCH=$CHANNEL&ENVIRONMENT=WEB&SIZE=1" | jq -r .versions[0].FileName) && \
echo File: $FILENAME && \
export URL=https://update.madfix.me/projects/MaterialDesignWebInterface/files/WEB/$FILENAME && \
echo URL: $URL && \
curl $URL -O && \
unzip $FILENAME -d /build/

# Copy to NGINX

RUN cp -R /build/dist/web/* /usr/share/nginx/html/
RUN ls /usr/share/nginx/html/
RUN rm -R /build/ && apt clean

# Meta

MAINTAINER Phyrone(phyrone@phyrone.de)
EXPOSE 80
VOLUME /usr/share/nginx/html/
