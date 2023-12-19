# Use Alpine Linux 3.19.0 as the base image
FROM alpine:3.19.0 as base

ENV LANG C.UTF-8

# Set environment variables for JDK version and build
ENV JDK_VERSION="17.0.9_9"
ENV JDK_VERSION_ENCODED="17.0.9%2B9"
# Encoded version for use in URL
ENV JDK_BUILD="OpenJDK17U-debugimage_aarch64_linux_hotspot_${JDK_VERSION}"
ENV JDK_ARCHIVE="${JDK_BUILD}.tar.gz"
ENV JDK_URL="https://github.com/adoptium/temurin17-binaries/releases/download/jdk-${JDK_VERSION_ENCODED}/${JDK_ARCHIVE}"

# Install dependencies necessary for fetching and setting up the JDK
RUN apk add --no-cache curl tar

# Download, extract the JDK, and list contents
RUN set -e && \
    set -x && \
    echo "Downloading JDK..." && \
    curl -LfsSo /tmp/${JDK_ARCHIVE} "${JDK_URL}" && \
    echo "Extracting JDK..." && \
    tar -xzf /tmp/${JDK_ARCHIVE} -C /tmp && \
    echo "Contents of /tmp after extraction:" && \
    ls -l /tmp
