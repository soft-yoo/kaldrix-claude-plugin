## Current MCP boundary

The MCP surface covers catalog resources, service recipes, estimate creation and copying, service positions,
sections, model review and quantity refresh, catalog price refresh, estimate-level markups and PDF export.
The UI's atomic spreadsheet editor is not exposed as an MCP operation: editing several positions in one
transaction, changing frozen composition details per position, recording actual quantities, setting KNR codes,
ordering sheet rows and editing custom sheet columns requires the application. `update_estimation_item`
only changes the fields declared in its schema; do not invent extra arguments or claim those sheet edits succeeded.


### Services for a selected BIM element

Use `list_element_service_quantities(projectId, elementId, recipeIds)` after `list_service_recipes` to find
which services accept the selected element. Send at most 200 distinct recipe IDs per call. The backend
calculates the drawing once and returns the exact scopes for every service from the same `modelVersion`.
An empty `sources` list means that service has no positive accepted quantity for this element.

A whole installation riser uses `elementType: INSTALLATION_RISER` and `floorId: null`. Its CO length
already includes both supply and return and the route allowance; WLZ has its own cable allowance.
Send the returned scopes unchanged to `add_catalog_service_to_estimate`. Choose whole-riser scopes or
its floor-segment scopes; using both duplicates the same physical quantities. The model review detects
that overlap between different positions. Within one position, `preview_estimate_position_scope` marks overlapping physical quantities as not ready; assignment and direct position writes reject them with `ESTIMATE_SCOPE_OVERLAP`. Choose the whole element or its parts. This read-only lookup does not create an estimate or add any positions.
