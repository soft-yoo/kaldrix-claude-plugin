## Token Budget

Read only needed resources. Prefer compact navigation before detail reads and follow returned next-tool guidance. Page through estimate rows using hasMore and nextPage; request component or detailed payloads only when needed. A compact page is not the complete estimate.

Tool response `_meta` includes `kaldrix/callId` for server log correlation and `kaldrix/backendDurationMs` for server processing from session dispatch to a ready response, including authorization and schema validation. This timing excludes network, gateway and client time; it cannot explain full connector latency by itself.
After a replay, the returned result retains its original modelVersion; read `get_project_detail` before planning another edit.
