# Otel collector sample

Uses OTel collector with the azure monitor exporter to export metrics to Azure monitor from apps using OTLP

## Step 1 - build a copy of the collector

```
go install go.opentelemetry.io/collector/cmd/builder@latest

builder --config=aca-builder.yaml
```

## step 2 - run the collector

```
./bin/otelcol-aca --config=config.yaml
```

Set your app to output OTLP/gRPC to http://localhost:5317

note: it's http not https.

A test project is in TestService

## Refs
https://github.com/open-telemetry/opentelemetry-collector/tree/main/cmd/builder
https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/exporter/azuremonitorexporter/README.md
https://opentelemetry.io/docs/collector/configuration/
