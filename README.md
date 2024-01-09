# Phoenix + Ecto OpenTelemetry + SigNoz Example

This is an example repository (largely based on the official otel elixir example application) that demo how to setup OpenTelemetry for a Phoenix application
with [`opentelemetry_phoenix`] and [`opentelemetry_ecto`].

- Export to OpenTelemetry Collector, which can then be configured to export to
  external services (SigNoz).

  ```
  Application --> OpenTelemetry Collector --> SigNoz
  ```

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

5. Visit your SigNoz instance and go to /traces to see the traces.
6. Run `docker compose down` to destroy the created resources.
