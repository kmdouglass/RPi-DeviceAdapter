FROM resin/raspberry-pi-python:3
MAINTAINER Kyle M. Douglass <kyle.m.douglass@gmail.com>

RUN [ "cross-build-start" ]

RUN useradd -ms /bin/bash tester \
    && mkdir -p /home/tester/userdata \
    && chown tester:tester /home/tester/userdata

RUN [ "cross-build-end" ]

# Environment configuration
USER tester:tester
VOLUME /home/tester/userdata
WORKDIR /home/tester/userdata
COPY --chown=tester:tester . .
RUN pip3 install -r requirements.txt --user \
    && pip3 install . --user

ENTRYPOINT ["/sbin/tini", "-s", "--"]
CMD ["/usr/local/bin/python", "-m", "unittest", "discover", "-s", "tacpho/adapters"]
