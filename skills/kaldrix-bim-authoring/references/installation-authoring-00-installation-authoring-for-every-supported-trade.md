# Installation authoring for every supported trade

Every physical write requires the reviewed `expectedModelVersion`. Individual element creation also requires `idempotencyKey`: use a unique stable key for one intent and reuse it only with identical input after an uncertain response. Example keys below are placeholders for independent intents; do not reuse them across real jobs. After a replay read the live project before another edit.


Use this workflow with the WORKSPACE tool profile. Tool availability and parameter schemas come from the runtime tool catalogue, not this guide. Requires the INSTALLATIONS company module and projects.read/projects.write scopes; estimates require ESTIMATES. Read `kaldrix://projects/structures-and-installations` for the longer house and estimate playbooks.
