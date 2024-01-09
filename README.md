# Phoenix + Ecto OpenTelemetry + SigNoz Example

This is an example repository (largely based on the officaial otel elixir example application) that demo how to setup OpenTelemetry for a Phoenix application
with [`opentelemetry_phoenix`][0] and [`opentelemetry_ecto`][1].

- Here we directly export to external services (SigNoz) that accept OTLP protocol.
  ```
  Application --> External Service
  ```

## Getting Stated

Sign up to SigNoz Cloud and get your ingest endpoint and access token from the settings.

Set up your :opentelemetry application config similarly to how it is in the runtime.exs file.

Edit the .env file to add the SIGNOZ env vars.

Assuming you already have Docker and Docker Compose installed:

1. Run `docker compose up -d` to start PostgreSQL.
2. Run deps get and ecto setup:
   ```
   mix deps.get
   mix ecto.setup
   ```
3. Start phoenix `OTEL_SERVICE_NAME=demo iex -S mix phx.server`

4. Browse to http://localhost:4000. Additionally, you can:

- Visit http://localhost:4000/posts to see how it works for Phoenix HTML
- Visit http://localhost:4000/users to see how it works for Phoenix LiveView

5. Visit your SigNoz instance, and go to /traces to see the traces.
6. Run `docker compose down` to destroy the created resources.
