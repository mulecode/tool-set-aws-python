FROM amazonlinux:2023

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set-aws-python"
LABEL org.opencontainers.image.description="Python 3.14.2 Tool-set"

ENV PYTHON_VERSION=3.14.2
ENV BLACK_VERSION=25.12.0
ENV PIP_VERSION=25.3

WORKDIR /opt/app

# hadolint ignore=DL3033
RUN yum -y update && \
    yum -y upgrade && \
    yum -y install \
     make \
     zip \
     tar \
     gzip \
     gcc \
     libffi-devel \
     openssl  \
     openssl-devel \
     bzip2-devel \
     libxslt \
     sqlite-devel \
     wget \
     zlib-devel \
     git && \
    yum -y clean all && \
    rm -rf /var/cache

# install python 3
RUN wget -q https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz && \
    tar -xvf Python-${PYTHON_VERSION}.tgz

WORKDIR /opt/app/Python-${PYTHON_VERSION}
RUN ./configure --enable-loadable-sqlite-extensions --with-ensurepip=install && make && make install && \
    pip3 install --no-cache-dir --upgrade pip==${PIP_VERSION} && \
    pip3 install --no-cache-dir black==${BLACK_VERSION}

WORKDIR /opt/app
RUN rm -rf Python-*

# Image command entry point
ENTRYPOINT ["python3"]
# # Default command
CMD ["--version"]
