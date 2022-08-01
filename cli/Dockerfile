FROM wordpress:cli

USER root
# Install make tool
USER root
RUN apk add openssh-client

RUN apk add --no-cache make
RUN apk add dos2unix --update-cache
COPY entrypoint.sh /scripts/
COPY Makefile /scripts/

# Make docker-compose wait for container dependencies be ready
# Add the wait script to the image
ENV WAIT_VERSION 2.7.2
ADD https://github.com/ufoscout/docker-compose-wait/releases/download/$WAIT_VERSION/wait /wait
RUN chmod +x /wait

# Add Makefile to scripts dir
RUN chmod +x /scripts/entrypoint.sh
RUN dos2unix /scripts/entrypoint.sh

ENTRYPOINT [ "/scripts/entrypoint.sh" ]
USER 33:33
CMD ["wp", "shell"]
