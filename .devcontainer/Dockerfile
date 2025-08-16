# .devcontainer/Dockerfile
FROM python:3.12-slim

ARG DEBIAN_FRONTEND=noninteractive

# Install system dependencies for Spark, Kafka, and compilation
RUN apt-get update && apt-get install -y --no-install-recommends \
    openjdk-11-jdk-headless \
    build-essential \
    curl \
    git \
    wget \
    gnupg \
    ca-certificates \
    libsasl2-dev \
    libssl-dev \
    liblz4-dev \
    librdkafka-dev \
    && rm -rf /var/lib/apt/lists/*

# Java env for PySpark / Glue
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH

# Set workdir
WORKDIR /workspace

# Install Python deps
COPY requirements.txt /tmp/requirements.txt
RUN python -m pip install --upgrade pip setuptools wheel \
    && pip install -r /tmp/requirements.txt \
    && rm -f /tmp/requirements.txt

# AWS CLI for local testing
RUN pip install awscli boto3

# Default shell
CMD ["/bin/bash"]