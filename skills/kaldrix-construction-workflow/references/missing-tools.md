## When a tool is missing

- Call `list_tool_profiles`: it reports the single `workspace` catalog, `activeToolNames` and `hiddenToolCount`. Compare these with the tools exposed by the client.
- Guides and catalogs read inside a connection are filtered the same way as `tools/list`. Markdown guides end with "Not available in this connection" and JSON resources carry `unavailableInThisConnection`: each entry names the hidden tool, the reason (`MISSING_PERMISSION`, `MODULE_DISABLED` or `COMPANY_TYPE`) and the requirement. Do not call those tools; explain the requirement to the user or use a visible alternative.
- If the client shows an older catalog after a server upgrade, refresh the connector catalog. Repeating the request does not load tool schemas.
- `UNKNOWN_TOOL` means the name is not registered; discover exact names instead of inventing them. `MISSING_SCOPE` and other permission refusals mean the person lacks that permission or did not approve it for this connection (see the next section), `MODULE_DISABLED` needs the company owner (company modules are an owner privilege), and company-type restrictions still apply. Another profile cannot bypass these checks.
- Never claim a model or estimate was created without a successful tool result.
