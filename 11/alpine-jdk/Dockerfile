FROM alpine:3.10.1 as base

LABEL app=openjdk-alpine
# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

ARG JDK="13"
ARG JDK_BUILD="27" 
ARG JAVA_AGENT="0.12.0"
ENV JDK_ARCHIVE="openjdk-${JDK}-ea+${JDK_BUILD}_linux-x64-musl_bin.tar.gz"
ENV JAVA_HOME=/jdk 


RUN set -e && \
    set -x && \
    wget https://download.java.net/java/early_access/alpine/${JDK_BUILD}/binaries/openjdk-${JDK}-ea+${JDK_BUILD}_linux-x64-musl_bin.tar.gz  && \
    wget https://download.java.net/java/early_access/alpine/${JDK_BUILD}/binaries/openjdk-${JDK}-ea+${JDK_BUILD}_linux-x64-musl_bin.tar.gz.sha256 && \
    echo "Verify checksum" && \
    echo "  ${JDK_ARCHIVE}" >> ${JDK_ARCHIVE}.sha256 && \
    sha256sum -c ${JDK_ARCHIVE}.sha256 && \
    tar -xzf ${JDK_ARCHIVE} && \
    mv /jdk-${JDK} /jdk && \
    mkdir /prometheus   && \
    wget  https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/${JAVA_AGENT}/jmx_prometheus_javaagent-${JAVA_AGENT}.jar -P /prometheus && \
    rm ${JDK_ARCHIVE} ${JDK_ARCHIVE}.sha256 && \
    rm ${JAVA_HOME}/lib/src.zip

FROM alpine:3.10.1
ARG JDK="13"
ARG JDK_BUILD="27"

LABEL  app=openjdk-alpine
# Default to UTF-8 file.encoding
ENV LANG C.UTF-8
COPY --from=base /jdk /jdk
COPY --from=base /prometheus /opt/prometheus 

ENV JAVA_HOME=/jdk
ENV PATH="$PATH:$JAVA_HOME/bin"

ENV JAVA_VERSION ${JDK}-ea+${JDK_BUILD}
ENV JAVA_ALPINE_VERSION ${JDK}~${JDK_BUILD}-1
