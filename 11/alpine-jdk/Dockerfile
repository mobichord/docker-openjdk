FROM mobichord/openjdk-alpine:11-jdk as base

LABEL app=openjdk-alpine
# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

ARG JDK="11"
ARG JDK_BUILD="28" 
ARG JAVA_AGENT="0.12.0"
ENV JAVA_HOME=/jdk-11


RUN set -e && \
    set -x && \
    mkdir /prometheus   && \
    wget  https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/${JAVA_AGENT}/jmx_prometheus_javaagent-${JAVA_AGENT}.jar -P /prometheus 

FROM alpine:3.10.1
ARG JDK="11"
ARG JDK_BUILD="28"

LABEL  app=openjdk-alpine
# Default to UTF-8 file.encoding
ENV LANG C.UTF-8
COPY --from=base /jdk-11 /jdk-11
COPY --from=base /prometheus /opt/prometheus 

ENV JAVA_HOME=/jdk-11
ENV PATH="$PATH:$JAVA_HOME/bin"

ENV JAVA_VERSION ${JDK}-ea+${JDK_BUILD}
ENV JAVA_ALPINE_VERSION ${JDK}~${JDK_BUILD}-1
