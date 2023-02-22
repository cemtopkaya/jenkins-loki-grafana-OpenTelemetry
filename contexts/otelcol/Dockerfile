# ----- Jenkins yansısı içinde çalışabilir ------ #
#FROM jenkins/jenkins:2.391-jdk11

# ----- VEYA sidecar olarak çalışabilir ------ #
FROM ubuntu:focal

RUN apt-get update && apt-get install -y curl

# OpenTelemetry ile Jenkins görevlerinin build edilmesinde elde edilecek günlükleri 
# LOKI'ye göndermek için 
# Send logs to Grafana Loki using the OpenTelemetry Collector
# https://grafana.com/docs/opentelemetry/collector/send-logs-to-loki/
RUN cd /tmp
RUN curl -O -L "https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/v0.71.0/otelcol-contrib_0.71.0_linux_amd64.deb"
RUN dpkg -i otelcol-contrib_0.71.0_linux_amd64.deb

WORKDIR /root/otelcol/
# Varsayılan olarak ekleniyor ancak ezilebilir
COPY config.yaml ./

# Günlüklerin toplandığı dizin
VOLUME [ "/log_folder" ]

CMD [ "otelcol-contrib", "--config", "config.yaml" ]