# SigNoz Phoenix + Ecto OpenTelemetry Example

This is a example repository (largely based on the officaial otel elixir example application) that demo how to setup OpenTelemetry for Phoenix application
with [`opentelemetry_phoenix`][0] and [`opentelemetry_ecto`][1].

Here, we are using [`opentelemetry_exporter`][2] to export the traces to [
OpenTelemetry Collector][3]. The collector in turn export the traces to [SigNoz].

## Getting Stated

Sign up to SigNoz Cloud and get your ingest endpoint and access token from the settings.

Tweak the otel-collector-config.yaml with your SigNoz ingest endpoint and access token as per: https://signoz.io/docs/tutorial/opentelemetry-binary-usage-in-virtual-machine/

By default, we only configure our OpenTelemetry collector to export traces to SigNoz Cloud.

Assuming you already have Docker and Docker Compose installed:

1. Run `docker compose up -d` to start the Phoenix application, PostgreSQL,
   OpenTelemetry Collector.
2. Run deps get and ecto setup:
   ```
   mix deps.get, ecto.setup
   ```
3. Start phoenix `OTEL_SERVICE_NAME=demo iex -S mix phx.server`

4. Browse to http://localhost:4000. Additionally, you can:

- Visit http://localhost:4000/posts to see how it works for Phoenix HTML
- Visit http://localhost:4000/users to see how it works for Phoenix LiveView

5. Visit your SigNoz instance and go to /traces to look the the traces.
6. Run `docker compose down` to destroy the created resources.

## Different ways to export traces

In general, there are 2 ways you can export your OpenTelemetry traces.

- Export to OpenTelemetry Collector, which can then be configured to export to
  external services.

  ```
  Application --> OpenTelemetry Collector --> SigNoz
                                      |-----> SigNoz
  ```

- Export directly to external services that accept OTLP protocol.

  ```
  Application --> External Service
  ```

[0]: https://hex.pm/packages/opentelemetry_phoenix
[1]: https://hex.pm/packages/opentelemetry_ecto
[2]: https://hex.pm/packages/opentelemetry_exporter
[3]: https://github.com/open-telemetry/opentelemetry-collector/
