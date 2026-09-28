# Installation and validation

## Prerequisites

- A non-production Power Platform environment with Dataverse
- Power Platform administration rights for environment and MCP configuration
- System Administrator or System Customizer rights for import and configuration
- Copilot Studio author access and approved runtime capacity
- Appropriate Power Apps entitlement for model-driven app users
- Approved Dataverse and Teams connection identities
- Organization-approved knowledge, DLP policies, security roles, and operational ownership

Confirm current Microsoft Product Terms and organizational policies rather than inferring entitlement from the presence of a service plan.

## Install

1. Download `AgentCoEFrontDoor_1_0_0_1.zip` from the GitHub release.
2. Select the target environment in Power Apps and import the solution as unmanaged.
3. Confirm import success and solution version `1.0.0.1`.
4. Publish all customizations.
5. Open the model-driven app, save and publish it once, then verify it launches.

This is a fresh-install release. It is not a downgrade path for an environment already using a higher solution version.

## Configure knowledge

1. Review the three files under `knowledge/`.
2. Replace every `[ORGANIZATION INPUT]` placeholder with approved local content.
3. Upload KB-01, KB-02, and KB-03 independently.
4. Name and describe each source according to its scope.
5. Confirm each source reaches Ready.
6. Test each source independently with the intended user identity.

Ready status alone does not prove that a source is retrievable. Knowledge indexing can vary by environment.

## Configure Dataverse MCP

1. Enable the GA Dataverse MCP environment feature.
2. Confirm Microsoft Copilot Studio App and Microsoft Copilot Studio App - OBO are allowed MCP clients.
3. Configure an approved `shared_commondataserviceforapps` connection.
4. Grant least-privilege access to read the catalogue and create/read intake requests.
5. Confirm the required read, search, describe, and create tools load.

If the imported MCP tool returns HTTP 403 after reauthentication, remove it and add a target-native Microsoft Dataverse MCP Server using a fresh target connection.

## Configure Teams

No fixed notification recipient is packaged.

Configure an approved connection and destination. Test both the actual recipient and actual message body. Use a deterministic Power Automate pattern if exact message content must be controlled.

## Minimum acceptance tests

1. **Import:** solution history shows success and version 1.0.0.1.
2. **Knowledge:** KB-01, KB-02, and KB-03 retrieve independently without source substitution.
3. **Reuse:** catalogue lookup occurs before a new intake is proposed.
4. **Intake:** only missing facts are collected and confirmation is required before writing.
5. **MCP:** required operations execute without HTTP 403 using least privilege.
6. **App:** a licensed, non-admin user can access only intended tables, views, forms, and operations.
7. **Security:** an unauthorized user cannot access the app or restricted Dataverse data.
8. **Teams:** only the approved destination receives the approved notification.
9. **Channel:** the approved end-user channel works end to end.
10. **Operations:** ownership, monitoring, capacity, support, and review dates are assigned.

## Known deployment considerations

- UX Agent Project support can vary by tenant.
- Unmanaged imports merge components and do not remove obsolete components.
- Knowledge sources that show Ready must still be tested for retrieval.
- Imported connection and MCP configuration can require target-native recreation.
- Non-production validation does not replace organization-specific security, licensing, performance, accessibility, or production-readiness testing.

