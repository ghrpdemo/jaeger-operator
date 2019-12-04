FROM centos:centos7

ENV OPERATOR=/usr/local/bin/jaeger-operator \
    USER_UID=1001 \
    USER_NAME=jaeger-operator

RUN INSTALL_PKGS=" \
      openssl \
      " && \
    yum install -y $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all && \
    mkdir /tmp/_working_dir && \
    chmod og+w /tmp/_working_dir

COPY scripts/* /scripts/

# install operator binary
COPY jaeger-operator ${OPERATOR}

COPY bin /usr/local/bin
RUN ls -la /usr/local/bin
RUN ls -la /bin
RUN ls -la /bin/sh
RUN sed -i -e 's/\r$//' /usr/local/bin/user_setup
RUN sed -i -e 's/\r$//' /usr/local/bin/entrypoint
RUN  /usr/local/bin/user_setup

#ENTRYPOINT ["/bin/bash", "-ec", "while : ; do echo '.'; sleep 5 ; done"]
ENTRYPOINT ["/usr/local/bin/entrypoint"]

USER ${USER_UID}
