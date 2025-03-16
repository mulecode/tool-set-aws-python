FROM amazonlinux:2

LABEL org.opencontainers.image.source="https://github.com/mulecode/tool-set-aws-python"
LABEL org.opencontainers.image.description="Python 3.11.11 Tool-set"

ENV PYTHON_VERSION=3.11.11
ENV BLACK_VERSION=25.1.0
ENV PIP_VERSION=25.0.1

WORKDIR /opt/app

# Updates yum
RUN yum -y update && \
    yum -y upgrade && \
    yum -y install make-3.82-24.amzn2 \
     zip-3.0-11.amzn2.0.2 \
     tar-1.26-35.amzn2 \
     gzip-1.5-10.amzn2 \
     gcc-7.3.1-17.amzn2 \
     libffi-devel-3.0.13-18.amzn2.0.2 \
     openssl11-1.1.1g-12.amzn2.0.23 \
     openssl11-devel-1.1.1g-12.amzn2.0.23 \
     bzip2-devel-1.0.6-13.amzn2.0.3 \
     libxslt-1.1.28-6.amzn2 \
     sqlite-devel-3.7.17-8.amzn2.1.2 \
     pango-1.42.4-4.amzn2 \
     wget-1.14-18.amzn2 \
     zlib-devel-1.2.7-19.amzn2.0.3 \
     git-2.47.1-1.amzn2.0.2 && \
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
