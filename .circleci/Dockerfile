# Dockerfile for the container CircleCI uses to build and test helios
FROM ubuntu:bionic

RUN apt-get -qq update && apt-get -qq install \
  # Required tools for primary containers that aren't already in bionic
  # https://circleci.com/docs/2.0/custom-images/#required-tools-for-primary-containers
  git ssh \
  # tools we need
  wget maven lsof jq python-minimal python-pip

# Download and validate checksum of openjdk-11
# Checksum from https://download.java.net/java/ga/jdk11/openjdk-11_linux-x64_bin.tar.gz.sha256
RUN wget --quiet https://download.java.net/java/ga/jdk11/openjdk-11_linux-x64_bin.tar.gz && \
  echo '3784cfc4670f0d4c5482604c7c513beb1a92b005f569df9bf100e8bef6610f2e openjdk-11_linux-x64_bin.tar.gz' > openjdk-11-sha256sum.txt && \
  sha256sum -c openjdk-11-sha256sum.txt

# Install openjdk-11
RUN tar -xzf openjdk-11_linux-x64_bin.tar.gz && \
  mkdir -p /usr/lib/jvm && \
  mv jdk-11 /usr/lib/jvm/openjdk-11 && \
  update-alternatives --install /usr/bin/java java /usr/lib/jvm/openjdk-11/bin/java 20000 && \
  update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/openjdk-11/bin/javac 20000

# Install codecov
RUN pip install codecov
