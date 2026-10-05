# Solution overview

Agent CoE Front Door is a reusable intake and triage pattern for organizations that want a governed entry point for agent discovery, guidance, self-build routing, and CoE-supported delivery.

The design principle is **answer first, intake second**. The agent should avoid creating a request when it can answer from approved knowledge, point to an existing catalogue item, or guide a maker through an approved self-service path.

![Agent CoE Front Door golden path](../assets/golden-path-visual.png)

## Golden path

Describe the business need, discover approved guidance and existing solutions, decide on reuse, self-build, or CoE support, capture a confirmed request only when needed, and manage demand in the triage app. The user can revise or stop before confirmation without creating a record.

## Operating model

The agent starts with self-service answers and catalogue discovery, then applies organization-specific routing. Structured intake follows only when review, visibility, or delivery support is needed. This keeps the front door lightweight while giving the CoE visibility into demand.

## Package boundary

![Agent CoE Front Door architecture](../assets/architecture-visual.png)

The release includes the Front Door agent, advisor and intake skills, Agent Catalogue, Agent Intake Request, and Tenant Agent Inventory tables, a model-driven triage app, knowledge templates, one disabled daily Power Platform Inventory API flow and connector, and Dataverse MCP. It does not include Agent 365. The adopting organization supplies approved knowledge, connections and identities, security roles, catalogue records, and operational ownership. If notifications are needed, configure a target-native Teams action with an approved destination after import.

Knowledge files, credentials, permissions, connection identities, Teams recipients, catalogue records, and production operations do not automatically travel with the solution package. The adopting organization must configure, approve, and test those values in its own environment.

## Main outcomes

| Outcome | Description |
|---|---|
| Reuse | The user is directed to an existing agent or approved answer where possible. |
| Guided self-build | A maker receives approved guidance and next steps without forcing a CoE delivery request. |
| CoE-supported intake | A structured request is created only after the user confirms the summary. |
| Portfolio visibility | CoE reviewers manage catalogue and intake records in the triage app. |

## Agent Catalogue vs Tenant Agent Inventory

These two Dataverse tables are different on purpose and must not be confused:

| | **Agent Catalogue** (`cat_agentcatalogue`) | **Tenant Agent Inventory** (`cat_tenantagentinventory`) |
| --- | --- | --- |
| Purpose | Curated, human-approved list of agents the CoE recommends | Technical discovery cache of agents found in the tenant |
| Populated by | People (CoE reviewers curate and approve entries) | The optional daily Power Platform Inventory API flow |
| Meaning of a row | This agent is approved and can be recommended | This agent exists in the tenant; approval is **not** implied |
| Shown to employees | Yes — as an approved recommendation | No — used internally as discovery evidence only |
| Source of truth for recommendations | Yes | No |

Tenant Agent Inventory provides technical discovery when the Power Platform Inventory API connection and daily flow are enabled. Agent Catalogue remains the curated source for approved recommendations. Front Door searches both through Dataverse and must describe an inventory match as discovery evidence rather than CoE approval. An agent in inventory but not in the catalogue has been *found*, not *approved*.

See [Power Platform Inventory API](POWER-PLATFORM-INVENTORY.md) for architecture, permissions, deployment, acceptance tests, and operations.
