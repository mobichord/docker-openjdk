# Use Alpine Linux 3.19.0 as the base image
FROM alpine:3.19.0 as base

ARG JAVA_AGENT="0.14.0"

RUN set -e && \
    set -x && \
    mkdir /prometheus   && \
    wget  https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/${JAVA_AGENT}/jmx_prometheus_javaagent-${JAVA_AGENT}.jar -P /prometheus

# Use azul/zulu-openjdk-alpine:17 as the JDK image
FROM azul/zulu-openjdk-alpine:17-jre

ENV LANG C.UTF-8
COPY --from=base /prometheus /opt/prometheus
