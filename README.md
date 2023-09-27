# Otel collector sample

Uses OTel collector with the azure monitor exporter to export metrics to Azure monitor from apps using OTLP

## Step 1 - build a copy of the collector

```
go install go.opentelemetry.io/collector/cmd/builder@latest

builder --config=aca-builder.yaml
```

## Step 2 - run the collector

```
./bin/otelcol-aca --config=config.yaml
```

Set your app to output OTLP/gRPC to http://localhost:5317

note: it's http not https.

## Step 3 - build and run test app
A test project is in TestService. It needs .NET 8 for the platform metrics. https://dotnet.microsoft.com/en-us/download/dotnet/8.0

```
cd TestService

dotnet restore
dotnet build

/bin/debug/net8.0/OtelTestService --Urls http://localhost:5000 --OTEL_EXPORTER_OTLP_ENDPOINT https://localhost:4317

curl http://localhost:5000/NestedGreeting?nestlevel=5
```

The service makes calls back to itself so you get nice traces. 


## Refs
https://github.com/open-telemetry/opentelemetry-collector/tree/main/cmd/builder
https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/exporter/azuremonitorexporter/README.md
https://opentelemetry.io/docs/collector/configuration/
