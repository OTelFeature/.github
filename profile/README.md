## Feature flags for your telemetry

**OTelFeature** controls OpenTelemetry instrumentation at runtime with [OpenFeature](https://openfeature.dev) flags. Turn tracing down while a service is healthy and back up when an incident starts, without a restart or a redeploy.

It started as the KubeCon + CloudNativeCon North America 2026 talk **[OpenFeature as a Control Plane for OpenTelemetry](https://otelfeature.github.io/presentation/)** by Simon Schrottner and Juliano Costa.

### What the flags do

- **Kill switch.** `otelEnabled: false` stops every span, live.
- **Less noise.** `telemetryLevel: IO` drops `INTERNAL` spans and keeps the `SERVER` and `CLIENT` edges.
- **Targeting.** OpenTelemetry semantic conventions become the evaluation context: drop health checks and DB spans, sample by environment, and sample more when the error rate climbs.

The decision happens in the SDK, where the span is born, not in the Collector after the data has already been sent.

### Repositories

| | |
|---|---|
| [poc](https://github.com/OTelFeature/poc) | The demo from the talk: two services, flagd, a Collector and a dashboard. Runs with only Docker. |
| [otelfeature-instrument](https://github.com/OTelFeature/otelfeature-instrument) | Python: a drop-in for `opentelemetry-instrument` with flag-controlled spans. |
| [otelfeature-java-extension](https://github.com/OTelFeature/otelfeature-java-extension) | Java: an extension for the OpenTelemetry Java agent. |

### Talk to us

This is a prototype with open questions. Should flags like `otelEnabled` or `traceSampleRatio` become conventions? Where should the contract between evaluation context and semantic conventions live? We'd like to hear from you:

- [Open an issue](https://github.com/OTelFeature/poc/issues/new) on the demo
- CNCF Slack ([invite](https://slack.cncf.io)): `#openfeature` and `#opentelemetry`
- [Simon](https://schrottner.at), a member of the OpenFeature Technical Committee, works at [Flagsmith](https://www.flagsmith.com/?utm_source=github&utm_medium=org-profile&utm_campaign=otelfeature&utm_content=org-profile). [Juliano](https://jcosta.dev), an OpenTelemetry Demo maintainer, works at [Dash0](https://www.dash0.com/?utm_source=github&utm_medium=org-profile&utm_campaign=otelfeature&utm_content=org-profile).
