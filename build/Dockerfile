FROM ubuntu:bionic

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

RUN apt-get update && \
    apt-get install --no-install-recommends -y transmission-daemon openjdk-8-jre-headless && \
    rm -rf /var/lib/apt/lists/*

COPY transmission-postprocess.sh /
COPY settings.json /etc/transmission-daemon/
ADD https://downloads.sourceforge.net/project/filebot/filebot/FileBot_4.7.9/filebot_4.7.9_amd64.deb ./
RUN dpkg -i filebot_4.7.9_amd64.deb

EXPOSE 9091

VOLUME ["/library"]
VOLUME ["/downloads"]

CMD ["/usr/bin/transmission-daemon", "-f", "-g", "/etc/transmission-daemon"]
