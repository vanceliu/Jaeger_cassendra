# Jaeger-cassendra
Examples on instrumenting python servers.  


## Quick Start


### 1. Run Jaeger

    docker-compose -f docker-compose.yaml up

It will create cassendra(storage) & Jaeger(UI & collector) service 

Test out Jaeger UI on [http://localhost:16686](http://localhost:16686)

### 2. Any Backend service

#### I. Craete virtual environment

    $ python -m venv venv
    $ source venv/bin/activate


#### II. Install OpenTelemetry, OTLP Exporter, and sdk


    
    $ pip install \
        opentelemetry-distro==0.57b0 \
        opentelemetry-exporter-otlp==1.36.0 \
        opentelemetry-instrumentation==0.57b0 \
        opentelemetry-sdk==1.36.0

#### III. Use automatic instrumentation

    $ opentelemetry-bootstrap -a install

The opentelemetry-bootstrap -a install command reads through the list of packages installed in your active site-packages folder, and installs the corresponding instrumentation libraries for these packages.

#### IV. Set environment for service to connect exporter 

    OTEL_SERVICE_NAME="${AP_SERVICE_NAME}"
    OTEL_EXPORTER_OTLP_ENDPOINT="http://0.0.0.0:4317"
    OTEL_TRACES_EXPORTER=otlp
    OTEL_METRICS_EXPORTER=none

set OTEL_METRICS_EXPORTER to none if not use metric
