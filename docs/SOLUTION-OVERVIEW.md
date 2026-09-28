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

The release includes the Front Door agent, advisor and intake skills, Agent Catalogue and Agent Intake Request tables, a model-driven triage app, knowledge templates, and Dataverse MCP and Teams tool definitions. The adopting organization supplies approved knowledge, connections and identities, security roles, a Teams destination, catalogue records, and operational ownership.

Knowledge files, credentials, permissions, connection identities, Teams recipients, catalogue records, and production operations do not automatically travel with the solution package. The adopting organization must configure, approve, and test those values in its own environment.

## Main outcomes

| Outcome | Description |
|---|---|
| Reuse | The user is directed to an existing agent or approved answer where possible. |
| Guided self-build | A maker receives approved guidance and next steps without forcing a CoE delivery request. |
| CoE-supported intake | A structured request is created only after the user confirms the summary. |
| Portfolio visibility | CoE reviewers manage catalogue and intake records in the triage app. |
