FROM alpine:3.8 as base

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

ARG JDK_BUILD="28"
ENV JDK_ARCHIVE="openjdk-11+${JDK_BUILD}_linux-x64-musl_bin.tar.gz"
ENV JAVA_HOME=/jdk-11

RUN set -e && \
    set -x && \
    wget https://download.java.net/java/early_access/alpine/${JDK_BUILD}/binaries/${JDK_ARCHIVE}  && \
    wget https://download.java.net/java/early_access/alpine/${JDK_BUILD}/binaries/${JDK_ARCHIVE}.sha256 && \
    echo "Verify checksum" && \
    echo "  ${JDK_ARCHIVE}" >> ${JDK_ARCHIVE}.sha256 && \
    sha256sum -c ${JDK_ARCHIVE}.sha256 && \
    tar -xzf ${JDK_ARCHIVE} && \
    rm ${JDK_ARCHIVE} ${JDK_ARCHIVE}.sha256 && \
    rm ${JAVA_HOME}/lib/src.zip

FROM alpine:3.8

# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

COPY --from=base /jdk-11 /jdk-11

ENV JAVA_HOME=/jdk-11
ENV PATH="$PATH:$JAVA_HOME/bin"

ENV JAVA_VERSION 11-ea+${JDK_BUILD}
ENV JAVA_ALPINE_VERSION 11~${JDK_BUILD}-1