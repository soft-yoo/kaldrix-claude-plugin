## Manifold settings

Plain installation routes and installation groups are no longer edited through MCP (KDX-177): use circuits
(`create_installation_circuit`, `update_installation_circuit` with `nodeEdit`) for connected cables and pipes. Existing
plain routes are listed in `get_floor_detail`.
Use `get_underfloor_manifold_settings` to inspect the saved manifold and current loop configuration before editing.
