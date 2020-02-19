FROM adoptopenjdk/openjdk13:x86_64-alpine-jre-13.0.1_9

# Install common Dojo scripts
ENV DOJO_VERSION=0.6.2

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && \
  apk add --no-cache tini bash shadow sudo git graphviz && \
  git clone --depth 1 -b ${DOJO_VERSION} https://github.com/kudulab/dojo.git /tmp/dojo_git &&\
  /tmp/dojo_git/image_scripts/src/install.sh && \
  rm -r /tmp/dojo_git &&\
  echo 'dojo ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

COPY resources/profile /home/dojo/.profile
COPY resources/bashrc /home/dojo/.bashrc

RUN chown dojo:dojo /home/dojo/.profile /home/dojo/.bashrc

ENTRYPOINT ["/sbin/tini", "-g", "--", "/usr/bin/entrypoint.sh"]
CMD ["/bin/bash"]