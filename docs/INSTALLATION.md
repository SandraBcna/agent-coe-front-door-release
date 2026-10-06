# Installation and validation

For the full owner-by-owner procedure, evidence expectations, golden-path scenarios, and troubleshooting, use the [deployment runbook](DEPLOYMENT-RUNBOOK.md). The [installer checklist](INSTALLER-CHECKLIST.md) provides a concise deployment record.

## Prerequisites

- A non-production Power Platform environment with Dataverse
- Power Platform administration rights for environment and MCP configuration
- System Administrator or System Customizer rights for import and configuration
- Copilot Studio author access and approved runtime capacity
- Appropriate Power Apps entitlement for model-driven app users
- Approved Dataverse and Teams connection identities
- An approved target-owned Entra application and delegated Power Platform Inventory API consent
- Organization-approved knowledge, DLP policies, security roles, and operational ownership

Confirm current Microsoft Product Terms and organizational policies rather than inferring entitlement from the presence of a service plan.

## Install

1. Use `release/AgentCoEFrontDoor_1_0_0_2.zip` from this checkout (not yet published; earlier draft builds imported into CDX, but these exact bytes have not been clean-imported).
2. Select the target environment in Power Apps and import the solution as unmanaged.
3. Confirm import success and solution version `1.0.0.2`.
4. Publish all customizations.
5. Open the model-driven app, save and publish it once, then verify it launches.

## Configure inventory

Inventory is optional and its single daily flow is disabled after import. Follow the [ordered Power Platform Inventory API setup](POWER-PLATFORM-INVENTORY.md): register a target-owned single-tenant app, consent delegated `ResourceQuery.Resources.Read`, configure connector OAuth and its generated redirect, create/test the signed-in connection, bind `cat_ppinventory` and Dataverse, run Flow checker, and verify two complete refreshes without duplicates before turning it on. Verify the Power Platform Agents, Copilot Studio, and Agent Builder views; Agent Builder needs a tenant with example records for live validation.

This is a fresh-install release. It is not a downgrade path for an environment already using a higher solution version.

## Configure knowledge

1. Review the three repository files under `knowledge/`; they are not embedded in the solution ZIP.
2. Replace every `[ORGANIZATION INPUT]` placeholder with approved local content.
3. If upgrading from an older unmanaged import, remove any inherited placeholder SharePoint source; this draft does not package one.
4. Upload approved KB-01, KB-02, and KB-03 independently, or connect equivalent approved sources with the same scopes. Do not share the agent with employees before knowledge retrieval and security checks pass.
5. Name and describe each source according to its scope.
6. Confirm each source reaches Ready.
7. Test each source independently with the intended user identity.

Ready status alone does not prove that a source is retrievable. Knowledge indexing can vary by environment.

Use the Copilot Studio designer for instruction and knowledge changes, then save and publish before testing in a new chat. Do not rely on direct Dataverse edits to bot records.

## Configure Dataverse MCP

1. Enable the GA Dataverse MCP environment feature.
2. Confirm Microsoft Copilot Studio App and Microsoft Copilot Studio App - OBO are allowed MCP clients.
3. Configure an approved `shared_commondataserviceforapps` connection.
4. Grant least-privilege access to read inventory and catalogue and create/read confirmed intake requests; do not grant ordinary users direct inventory access.
5. Confirm the required read, search, describe, and create tools load.

If the imported MCP tool returns HTTP 403, first create/select a fresh target-native Dataverse connection on the existing tool and save the agent. If its tool catalogue still fails to load, remove and recreate the tool in the target.

## Configure Teams

No Teams action or recipient is packaged. Create a target-native **Post message in a chat or channel** action only after the destination and connection owner approve it; this avoids an unresolved imported connection reference that otherwise prevents agent preview.

Configure an approved connection and destination. Test both the actual recipient and actual message body. Use a deterministic Power Automate pattern if exact message content must be controlled.

## Minimum acceptance tests

1. **Import:** solution history shows success and version 1.0.0.2.
2. **Knowledge:** KB-01, KB-02, and KB-03 retrieve independently without source substitution.
3. **Reuse:** catalogue lookup occurs before a new intake is proposed.
4. **Intake:** only missing facts are collected and confirmation is required before writing.
5. **MCP:** required operations execute without HTTP 403 using least privilege.
6. **App:** a licensed, non-admin user can access only intended tables, views, forms, and operations.
7. **Security:** an unauthorized user cannot access the app or restricted Dataverse data.
8. **Teams:** only the approved destination receives the approved notification.
9. **Channel:** the approved end-user channel works end to end.
10. **Operations:** ownership, monitoring, capacity, support, and review dates are assigned.
11. **Inventory:** the Power Platform API refresh succeeds twice with complete, unique results and source-scoped success-only stale cleanup; the schedule remains Off until acceptance.

## Known deployment considerations

- UX Agent Project support can vary by tenant.
- Unmanaged imports merge components and do not remove obsolete components.
- Knowledge sources that show Ready must still be tested for retrieval.
- Imported connection and MCP configuration can require target-native recreation.
- The imported parent instructions may be empty: restore them in Copilot Studio, save, and reopen before relying on the agent; maker preview does not prove non-admin employee isolation.
- Non-production validation does not replace organization-specific security, licensing, performance, accessibility, or production-readiness testing.

## Additional support

- [Deployment runbook](DEPLOYMENT-RUNBOOK.md)
- [Installer checklist](INSTALLER-CHECKLIST.md)
- [Public disclaimer and adopter responsibilities](../NOTICE.md)
- [Security reporting](../SECURITY.md)
