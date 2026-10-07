# Unshadow memory for Hermes

This is the minimal native directory provider. The main Unshadow repository stays private; export this directory as the public integration repository. Its implementation is provided by the declared `unshadow==0.4.0` dependency, not copied from a temporary venv.

After the SDK release and public wrapper repository are published, install the wrapper with Hermes' plugin manager using the repository URL **pinned to its full commit SHA**, then run `hermes memory setup` and select `unshadow`. Use the actual generated release manifest/install command; do not substitute `main` or an invented commit. Publication status is recorded in the P16 evidence ledger.

For a local development check place the reviewed directory at `$HERMES_HOME/plugins/unshadow/`, then select `unshadow` in `hermes memory setup`. The directory layout is supported by both tested hosts; do not assume `hermes plugins install` accepts an arbitrary local path. Use its Git repository URL and `--ref <full-SHA>` for the published wrapper. PM-managed Hermes installations prepare the declared dependency through their plugin manager; do not pip-install into Hermes' selected environment. Owner-managed environments may declaratively include the SDK's existing class entry points.

Set `UNSHADOW_API_KEY` through the host's secret configuration. It selects one project. Fresh write keys enable automatic recall and capture; readonly keys recall only. Explicit `auto_capture=false` and `auto_recall=false` survive configuration changes. Optional non-secret settings are in the active profile's `unshadow.json`:

```json
{"api_url":"https://api.unshadow.dev/v2","auto_capture":true,"auto_recall":true,"token_budget":1200}
```

Completed primary turns own capture. Compression and session-end do not re-save the whole transcript. Persistent sanitized outboxes survive an offline restart; failed writes remain visible. Child/cron runs cannot automatically capture. Recalled source text and assistant suggestions are advisory evidence, never action authorization.

`diagnostics()` reports provider/Python, project, grants, pending entries, last durable acknowledgement and safe error codes without credentials or conversation content. Session end/shutdown reports undrained work rather than silently discarding it. Existing `lattice-hermes` imports and class entry points remain supported.
