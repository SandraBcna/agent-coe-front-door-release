# Deployment runbook

This runbook takes an installer from environment preparation through operational handoff. Use it with the [installer checklist](INSTALLER-CHECKLIST.md) and record evidence in your organization's approved system.

## 1. Understand the package boundary

### Included

- Agent CoE Front Door Copilot Studio agent
- Agent Catalogue and Agent Intake Request Dataverse tables
- Tenant Agent Inventory Dataverse table and filtered views
- Disabled daily Power Platform inventory refresh flow, custom connector, and connection reference
- Agent CoE Triage model-driven app and site map
- Advisor and intake skills
- Microsoft Dataverse MCP tool definition
- Optional target-native Teams notification setup (no imported Teams action)
- Microsoft product-documentation knowledge definitions
- Web resources, icons, and intake-status logic
- UX Agent Project files for the triage dashboard
- Three organization-neutral knowledge templates in the repository, not the solution ZIP

### Not included

- Approved organization policy or licensing advice
- A production SharePoint knowledge library
- KB-01, KB-02, or KB-03 knowledge attachments; attach approved versions after import
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
| Identity administrator | Approve delegated Power Platform Inventory API permission, connector identity, and credential rotation |

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
11. If inventory is enabled, approve a dedicated Entra application with delegated `ResourceQuery.Resources.Read`.

Do not import until required configuration items have owners and target values.

## 5. Import the solution

1. Use `AgentCoEFrontDoor_1_0_0_2.zip` from the local draft release directory; it is not published on GitHub.
2. Verify its SHA-256:

   `5C97F04C01D8A437F82A297F8A7B64086BF3B3D83E3B17B6918B64AD7E2971C3`

3. In `make.powerapps.com`, select the target environment.
4. Open **Solutions** and import the ZIP as an unmanaged solution.
5. Map the Dataverse connection reference when prompted. The Power Platform Inventory API reference remains unbound until its target-owned OAuth setup; no Teams action or reference is bundled.
6. Wait for **Solution imported successfully**.
7. Confirm:
   - unique name: `AgentCoEFrontDoor`
   - version: `1.0.0.2` (draft package; an earlier build imported into CDX, but the latest ZIP without knowledge attachments has not had a fresh import)
8. Open solution history and capture the successful import result.
9. Publish all customizations.

This is a fresh-install release. Do not use it to downgrade an environment already carrying a higher solution version.
After import, inspect the parent agent instructions in Copilot Studio. Two fresh CDX imports left them empty despite their presence in the solution ZIP; restore the packaged instructions through the designer, save, reopen, and verify persistence before testing. This is a known portability gate, not an optional customization.

## 6. Configure Power Platform inventory

Follow the ordered [Power Platform Inventory API setup and acceptance procedure](POWER-PLATFORM-INVENTORY.md): obtain delegated permission and consent; configure target OAuth and generated Web redirect; create/test the signed-in connection; bind both references; confirm flow checker; test two complete refreshes and failure-safe cleanup; then enable the single daily schedule. The package contains no Agent 365 flow or connector. An unmanaged import into an environment with an older provider does not remove its flow or rows; turn the old schedule off and review its components separately.

## 7. Configure organization knowledge

The agent maps knowledge by scope:

| File | Scope |
|---|---|
| KB-01 Licensing and Capacity | Licensing, entitlements, capacity, and escalation |
| KB-02 Governance and Routing | Governance gates, risk, approvals, and support route |
| KB-03 Naming, Ownership, and Catalogue | Naming, lifecycle ownership, review, and catalogue standards |

1. Copy the three template files from the repository's `knowledge/` directory into an approved working location. They are not in the solution ZIP.
2. Replace every `[ORGANIZATION INPUT]` placeholder.
3. Obtain approval from the knowledge owner.
4. If upgrading from an earlier unmanaged version, remove any inherited placeholder SharePoint knowledge source.
5. Upload each approved file independently to the agent, or place approved content in a governed SharePoint library. Do not share the agent or enable an employee-facing channel before this setup and the three retrieval tests pass.
6. Give each source its KB identifier and a scope-specific description.
7. Confirm each source reaches Ready.
8. Save and publish the agent.
9. Test each KB independently with the intended end-user identity.
10. Confirm the answer does not substitute content from a different KB.
11. Record the owner, approval date, and next review date.

Ready status alone is not proof of retrieval. Indexing behavior can vary by environment.

Make instruction and knowledge changes through Copilot Studio, then save and publish. Direct Dataverse edits can appear in an export while the designer republishes an older cached configuration.

In earlier clean-environment validation, all three attached files reached Ready and returned their expected independent scopes after an inherited placeholder source was removed, the agent was saved and published, and indexing completed. This draft packages neither those files nor the placeholder source.

## 8. Configure Dataverse MCP

1. Open the Microsoft Dataverse MCP Server tool in the agent.
2. Bind it to an approved target connection using `shared_commondataserviceforapps`.
   A fresh target-native connection resolved HTTP 403 on an imported tool in CDX without removing the tool; save the agent and reopen the tool to confirm its permissions load.
3. Grant only the permissions required to:
   - read `cat_tenantagentinventory` for discovery, without exposing that table directly to ordinary employees;
   - read `cat_agentcatalogue`;
   - create `cat_agentintakerequest`; and
   - read back `cat_agentintakerequest`.
4. Confirm the read, search, describe, and create tool catalogue loads.
5. Test a catalogue read without changing data.
6. Create a TEST-prefixed intake only after reviewing the confirmation summary.
7. Read the created record back and verify its values.

### If the imported MCP tool returns HTTP 403

An imported connection can appear connected but still fail the tool-catalogue request. Do not broaden its permissions to bypass an authorization error.

1. Confirm the MCP feature and both allowed clients again.
2. Create or select a fresh target-native `shared_commondataserviceforapps` connection **on the imported MCP tool**.
3. Save, reload, and confirm its permitted tool catalogue loads; this resolved HTTP 403 in CDX without replacing the tool.
4. Only if it still fails, remove the imported tool and add a new target-native Microsoft Dataverse MCP Server with the approved connection.
5. Repeat the least-privilege inventory/catalogue read and confirmed TEST create/read-back checks before publishing.

Before giving employees access, verify whether the MCP uses a shared account or end-user credentials. Maker-admin preview cannot prove the safety of a shared administrator connection. Use approved least-privilege connection/table permissions and a non-admin identity test; if the restricted inventory cannot be isolated, keep the agent CoE-only.

## 9. Configure Teams notification

No recipient is packaged.

1. Decide whether notifications are needed; the package intentionally omits the imported Teams action, which can carry a broken cross-environment connection reference and prevent agent preview.
2. If needed, create a target-native **Post message in a chat or channel** Teams action in Copilot Studio.
3. Set an explicit, approved destination, never an AI-selected recipient.
4. Select the approved connection identity and decide whether the destination is a user, chat, or channel.
5. Obtain approval from the destination owner before testing.
6. Use a TEST-prefixed intake and a non-sensitive message.
7. Verify:
   - the actual recipient;
   - the exact received message;
   - no unintended recipient received it; and
   - retries do not create unacceptable duplicates.

The validated connector delivered successfully, but generative composition expanded the intended test text. Use a locked Power Automate template or equivalent deterministic pattern when exact content control is required.

## 10. Publish and test the model-driven app

1. Open **Agent CoE Triage** in the solution.
2. Save and publish it once after import.
3. Launch the app.
4. Verify:
   - Agent Intake Triage Dashboard;
   - Agent Catalogues navigation;
   - Agent Intake Requests navigation;
   - Tenant Agent Inventory navigation;
   - Active, Power Platform Agents, Copilot Studio, and Agent Builder inventory views;
   - views and forms;
   - filters and search;
   - the TEST intake record; and
   - intended status-update behavior.
5. Assign the approved Power Apps entitlement and least-privilege role to a non-admin tester.
6. Repeat intended read and write operations as that tester.
7. Verify an unauthorized user cannot open the app or restricted data.

Administrator testing alone is not sufficient evidence of correct security.

## 11. Run the golden path

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

## 12. Acceptance and release gates

| Area | Pass condition |
|---|---|
| Import | Solution history is successful and version is 1.0.0.2 |
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
| Inventory | Power Platform API complete paginated count, idempotent upsert, source-scoped success-only cleanup, and filtered views are verified |

A successful solution import is not a deployment approval. Release only when the organization's required gates pass.

## 13. Upgrade and cleanup guidance

Unmanaged imports merge components and do not remove obsolete objects.

When upgrading an earlier environment, inspect and remove or disconnect:

- old personal-site knowledge sources;
- obsolete knowledge files or combined TEST packs;
- unused Power Platform for Admins V2 connection references;
- fixed or obsolete Teams recipients;
- connections owned by former installers; and
- duplicate or superseded MCP tools.
- an inherited Agent 365 connector, connection reference, flow, and stale rows from an earlier unmanaged import, if applicable (turn the old flow Off before removal).

Back up the target solution and configuration evidence before changes.

## 14. Operational handoff

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


## 15. Troubleshooting

| Symptom | Likely cause | Resolution |
|---|---|---|
| MCP tool returns HTTP 403 | Imported connection ACL or wrong connector variant | Confirm allowed clients and bind a fresh target-native `shared_commondataserviceforapps` connection; recreate the tool only if its catalogue still fails to load |
| MCP tool catalogue is empty | Feature, client allow-list, connection, or reload issue | Recheck feature and clients, authenticate, save, and reload the agent |
| Knowledge shows Ready but is not retrieved | Environment-specific indexing or scope issue | Upload independently, align names/descriptions, publish, wait for indexing, and test each KB separately |
| Agent uses the wrong KB | Ambiguous source descriptions or instruction map | Tighten source descriptions and enforce the KB scope map |
| App Play is unavailable or fails | App not saved/published after import | Open the app designer, save and publish once, then relaunch |
| Dashboard is missing | UX Agent Project unsupported or not exposed | Confirm tenant support; treat the dashboard as optional until verified |
| Imported Teams tool says "Can't save this tool. Try again" | Imported connector ACL or wrong connector variant | Copy its name and Description for AI, remove it, recreate it in the target with **Post message in a chat or channel**, restore the approved details, then follow Configure Teams notification; this draft package does not include the imported action |
| Teams message reaches wrong place | Generative recipient selection or stale action | Use an explicit destination and recreate the action in the target |
| Teams body differs from approved text | Generative message composition | Use a deterministic Power Automate template |
| Removed items reappear after upgrade | Unmanaged solution merge behavior | Perform documented post-upgrade cleanup |
| Inventory count is lower than the connector result | Incomplete paging or a failed upsert | Confirm the custom connector returns the complete collection, inspect the failed action, and do not run stale cleanup |
| Repeat refresh creates more rows | The environment and resource name do not map consistently to Resource ID | Check the `pp:<environmentId>:<name>` upsert key and complete pagination before cleanup |
| Power Platform Inventory API connection cannot be created | Placeholder OAuth values remain, the installer is not an app owner, or admin consent is missing | Have an authorized identity owner configure the imported connector, add its generated redirect URI, grant delegated `ResourceQuery.Resources.Read`, then create and bind the connection |
| Connection reference looks set but flow says Invalid connection | The binding was not committed | Reopen the reference, choose the authorized connection, click Save **and** confirm Save changes; reopen to verify |
| Query action has missing TableName/Clauses/Top or literal `@@variables('SkipToken')` | Imported body shape or typed designer expression | Re-enter the flattened query fields and insert the SkipToken variable using dynamic content; save, reopen, and run Flow checker |
| Inventory-only or draft records appear in employee answer | Shared account rights or unverified audience; instructions are not an access boundary | Disable the employee channel, restrict Dataverse/MCP rights and verify with non-admin and unauthorized identities before republishing |
| Organization knowledge points to an example SharePoint site | An older unmanaged import left an inherited placeholder source | Remove that source and attach approved KB-01, KB-02, and KB-03 files or an approved governed library |
| Agent still searches the removed placeholder source | The published runtime retained an older knowledge binding | Remove the source in the Studio designer, save, publish, start a new chat, and repeat independent KB retrieval tests after indexing |

## 16. Support boundary

This repository does not provide a support SLA. Before raising a public issue:

1. Remove all sensitive data and tenant identifiers.
2. Confirm the problem is in this template rather than a Microsoft product or service.
3. Include the solution version, high-level reproduction steps, and sanitized error text.
4. Use private vulnerability reporting for potential template vulnerabilities.
5. Use Microsoft support or MSRC channels for Microsoft product or service issues.
