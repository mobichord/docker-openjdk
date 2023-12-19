FROM alpine:3.12 as base

ARG JAVA_AGENT="0.14.0"

RUN set -e && \
    set -x && \
    mkdir /prometheus   && \
    wget  https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/${JAVA_AGENT}/jmx_prometheus_javaagent-${JAVA_AGENT}.jar -P /prometheus

FROM openjdk:15-jdk-alpine
ENV LANG C.UTF-8
COPY --from=base /prometheus /opt/prometheus 