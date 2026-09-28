# Deployment runbook

This runbook takes an installer from environment preparation through operational handoff. Use it with the [installer checklist](INSTALLER-CHECKLIST.md) and record evidence in your organization's approved system.

## 1. Understand the package boundary

### Included

- Agent CoE Front Door Copilot Studio agent
- Agent Catalogue and Agent Intake Request Dataverse tables
- Agent CoE Triage model-driven app and site map
- Advisor and intake skills
- Microsoft Dataverse MCP tool definition
- Configurable Microsoft Teams notification tool definition
- Microsoft product-documentation knowledge definitions
- Web resources, icons, and intake-status logic
- UX Agent Project files for the triage dashboard
- Three organization-neutral knowledge templates

### Not included

- Approved organization policy or licensing advice
- A production SharePoint knowledge library
- A fixed Teams recipient
- Credentials, connection secrets, or target identities
- Production security roles or user assignments
- Copilot Studio capacity or Power Apps licensing
- Production monitoring, support, or change-management processes

The installing organization owns every target-specific value and approval.

## 2. Assign owners

Assign named owners before import.

| Role | Minimum responsibility |
|---|---|
| Power Platform administrator | Select the environment; confirm Dataverse, capacity, DLP, MCP feature, and allowed clients |
| Solution installer | Import the solution, bind connections, publish customizations, and capture evidence |
| Copilot Studio author | Configure knowledge and tools, publish the agent, run evaluations, and configure channels |
| Dataverse security owner | Create and test least-privilege roles for catalogue, intake, and app access |
| Knowledge owner | Approve KB-01, KB-02, and KB-03 content and manage review dates |
| Teams owner | Approve the connection identity, destination, message pattern, and lifecycle |
| Business acceptance owner | Approve test evidence and the deployment decision |
| Operational support owner | Own monitoring, incidents, capacity, changes, and periodic review |

## 3. Complete licensing and capacity review

Confirm the target organization's current agreements and Microsoft Product Terms. Do not infer entitlement from the presence of a service plan.

Review:

- Copilot Studio authoring rights for makers
- Copilot Studio runtime capacity, Copilot Credits, or approved pay-as-you-go
- Power Apps entitlement for model-driven app users
- Microsoft 365 and Teams rights for selected channels and notifications
- Dataverse database, file, and log capacity
- Power Platform request capacity
- Dataverse and Teams connector rights for connection identities

Record who approved the decision and when it must be reviewed.

## 4. Prepare the target environment

1. Use a non-production environment with Dataverse in Ready state.
2. Confirm the intended region and data residency.
3. Review DLP policies covering Dataverse, Teams, SharePoint, and Copilot Studio.
4. Enable the GA Dataverse MCP environment feature.
5. Confirm both allowed MCP clients are active:
   - Microsoft Copilot Studio App
   - Microsoft Copilot Studio App - OBO
6. Create approved Dataverse and Teams connections.
7. Decide whether direct file knowledge or governed SharePoint knowledge will be used.
8. Confirm whether UX Agent Project components are supported if the dashboard is required.
9. Identify a licensed non-admin acceptance tester.
10. Capture screenshots or exported configuration evidence under organizational policy.

Do not import until required configuration items have owners and target values.

## 5. Import the solution

1. Download `AgentCoEFrontDoor_1_0_0_1.zip` from the GitHub release.
2. Verify its SHA-256:

   `08A63739B3B7518877F313C05C01701FAB6F0B7E8D90CFFF03334A8D551ECFF0`

3. In `make.powerapps.com`, select the target environment.
4. Open **Solutions** and import the ZIP as an unmanaged solution.
5. Map the Dataverse and Teams connection references when prompted.
6. Wait for **Solution imported successfully**.
7. Confirm:
   - unique name: `AgentCoEFrontDoor`
   - version: `1.0.0.1`
8. Open solution history and capture the successful import result.
9. Publish all customizations.

This is a fresh-install release. Do not use it to downgrade an environment already carrying a higher solution version.

## 6. Configure organization knowledge

The agent maps knowledge by scope:

| File | Scope |
|---|---|
| KB-01 Licensing and Capacity | Licensing, entitlements, capacity, and escalation |
| KB-02 Governance and Routing | Governance gates, risk, approvals, and support route |
| KB-03 Naming, Ownership, and Catalogue | Naming, lifecycle ownership, review, and catalogue standards |

1. Copy the three files from `knowledge/` into an approved working location.
2. Replace every `[ORGANIZATION INPUT]` placeholder.
3. Obtain approval from the knowledge owner.
4. Upload each file independently to the agent, or place approved content in a governed SharePoint library.
5. Give each source its KB identifier and a scope-specific description.
6. Confirm each source reaches Ready.
7. Save and publish the agent.
8. Test each KB independently with the intended end-user identity.
9. Confirm the answer does not substitute content from a different KB.
10. Record the owner, approval date, and next review date.

Ready status alone is not proof of retrieval. Indexing behavior can vary by environment.

## 7. Configure Dataverse MCP

1. Open the Microsoft Dataverse MCP Server tool in the agent.
2. Bind it to an approved target connection using `shared_commondataserviceforapps`.
3. Grant only the permissions required to:
   - read `cat_agentcatalogue`;
   - create `cat_agentintakerequest`; and
   - read back `cat_agentintakerequest`.
4. Confirm the read, search, describe, and create tool catalogue loads.
5. Test a catalogue read without changing data.
6. Create a TEST-prefixed intake only after reviewing the confirmation summary.
7. Read the created record back and verify its values.

### If the imported MCP tool returns HTTP 403

Reauthentication may not repair an inherited connector ACL.

1. Confirm the MCP feature and both allowed clients again.
2. Remove the imported MCP tool from the target agent.
3. Add a new target-native Microsoft Dataverse MCP Server.
4. Create or select a fresh `shared_commondataserviceforapps` connection.
5. Save and reload the agent.
6. Confirm the tool catalogue loads.
7. Repeat the least-privilege read and create tests.
8. Republish the agent.

Do not broaden permissions merely to bypass an authorization error.

## 8. Configure Teams notification

No recipient is packaged.

1. Open the Teams notification tool.
2. Replace AI-filled recipient behavior with an approved explicit destination.
3. Recreate the Teams action in the target environment when required.
4. Select the approved connection identity.
5. Decide whether the destination is a user, chat, or channel.
6. Obtain approval from the destination owner before testing.
7. Use a TEST-prefixed intake and a non-sensitive message.
8. Verify:
   - the actual recipient;
   - the exact received message;
   - no unintended recipient received it; and
   - retries do not create unacceptable duplicates.

The validated connector delivered successfully, but generative composition expanded the intended test text. Use a locked Power Automate template or equivalent deterministic pattern when exact content control is required.

## 9. Publish and test the model-driven app

1. Open **Agent CoE Triage** in the solution.
2. Save and publish it once after import.
3. Launch the app.
4. Verify:
   - Agent Intake Triage Dashboard;
   - Agent Catalogues navigation;
   - Agent Intake Requests navigation;
   - views and forms;
   - filters and search;
   - the TEST intake record; and
   - intended status-update behavior.
5. Assign the approved Power Apps entitlement and least-privilege role to a non-admin tester.
6. Repeat intended read and write operations as that tester.
7. Verify an unauthorized user cannot open the app or restricted data.

Administrator testing alone is not sufficient evidence of correct security.

## 10. Run the golden path

Use non-sensitive TEST data.

### Reuse scenario

Ask whether an existing agent can answer a defined policy question.

Pass when:

- the catalogue is checked first;
- a verified reusable match is prioritized;
- a new intake is not created unnecessarily; and
- any catalogue gap is stated rather than invented.

### Licensing scenario

Ask what license is required to create and use an agent.

Pass when:

- the answer is grounded in approved KB-01;
- local gaps or approvals are disclosed;
- no entitlement is invented; and
- no intake is created unless requested.

### Governed intake scenario

Describe an agent that reads and writes to a business system and request CoE support.

Pass when:

- the catalogue is checked;
- KB-02 is used for governance and routing;
- only missing facts are requested;
- a clear confirmation summary is displayed;
- no record is written before explicit confirmation;
- the record is created with the intended status and route;
- the record is read back; and
- no notification is sent unless requested and configured.

## 11. Acceptance and release gates

| Area | Pass condition |
|---|---|
| Import | Solution history is successful and version is 1.0.0.1 |
| Knowledge | KB-01, KB-02, and KB-03 retrieve independently for intended users |
| Reuse | Catalogue is checked and unnecessary intake is avoided |
| Intake | Confirmation is required before a valid TEST record is created |
| MCP | Required operations execute without HTTP 403 using least privilege |
| Teams | Only the approved destination receives the approved message |
| App | Licensed non-admin users can perform only intended operations |
| Security | Unauthorized users cannot access the app or restricted data |
| Evaluation | Representative evaluations meet organization-approved thresholds |
| Channel | Approved end-user channel works end to end |
| Operations | Support, capacity, monitoring, review, and change owners are assigned |

A successful solution import is not a deployment approval. Release only when the organization's required gates pass.

## 12. Upgrade and cleanup guidance

Unmanaged imports merge components and do not remove obsolete objects.

When upgrading an earlier environment, inspect and remove or disconnect:

- old personal-site knowledge sources;
- obsolete knowledge files or combined TEST packs;
- unused Power Platform for Admins V2 connection references;
- fixed or obsolete Teams recipients;
- connections owned by former installers; and
- duplicate or superseded MCP tools.

Back up the target solution and configuration evidence before changes.

## 13. Operational handoff

Document:

- business, technical, knowledge, security, and support owners;
- connection identities and renewal process;
- knowledge review dates;
- capacity monitoring and alert thresholds;
- incident and escalation route;
- release and rollback approach;
- evaluation schedule;
- channel ownership;
- access-review schedule; and
- known limitations accepted by the business owner.

Keep production evidence outside this public repository.

## 14. Troubleshooting

| Symptom | Likely cause | Resolution |
|---|---|---|
| MCP tool returns HTTP 403 | Imported connector ACL or wrong connector variant | Confirm allowed clients, then recreate the tool and fresh `shared_commondataserviceforapps` connection |
| MCP tool catalogue is empty | Feature, client allow-list, connection, or reload issue | Recheck feature and clients, authenticate, save, and reload the agent |
| Knowledge shows Ready but is not retrieved | Environment-specific indexing or scope issue | Upload independently, align names/descriptions, publish, wait for indexing, and test each KB separately |
| Agent uses the wrong KB | Ambiguous source descriptions or instruction map | Tighten source descriptions and enforce the KB scope map |
| App Play is unavailable or fails | App not saved/published after import | Open the app designer, save and publish once, then relaunch |
| Dashboard is missing | UX Agent Project unsupported or not exposed | Confirm tenant support; treat the dashboard as optional until verified |
| Teams message reaches wrong place | Generative recipient selection or stale action | Use an explicit destination and recreate the action in the target |
| Teams body differs from approved text | Generative message composition | Use a deterministic Power Automate template |
| Removed items reappear after upgrade | Unmanaged solution merge behavior | Perform documented post-upgrade cleanup |

## 15. Support boundary

This repository does not provide a support SLA. Before raising a public issue:

1. Remove all sensitive data and tenant identifiers.
2. Confirm the problem is in this template rather than a Microsoft product or service.
3. Include the solution version, high-level reproduction steps, and sanitized error text.
4. Use private vulnerability reporting for potential template vulnerabilities.
5. Use Microsoft support or MSRC channels for Microsoft product or service issues.

