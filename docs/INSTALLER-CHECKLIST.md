# Installer checklist

Copy this checklist into the organization's approved deployment record. Do not enter production identities, URLs, secrets, or sensitive evidence in the public repository.

## Planning

- [ ] Business acceptance owner assigned
- [ ] Power Platform administrator assigned
- [ ] Solution installer assigned
- [ ] Copilot Studio author assigned
- [ ] Dataverse security owner assigned
- [ ] Knowledge owner assigned
- [ ] Teams owner assigned
- [ ] Operational support owner assigned
- [ ] Non-production environment selected
- [ ] Region and data residency approved
- [ ] Licensing and capacity approved
- [ ] DLP and connector policy reviewed

## Environment

- [ ] Dataverse is Ready
- [ ] GA Dataverse MCP feature enabled
- [ ] Microsoft Copilot Studio App allowed
- [ ] Microsoft Copilot Studio App - OBO allowed
- [ ] Approved Dataverse connection created
- [ ] Approved Teams connection created
- [ ] Power Platform inventory enabled or intentionally left Off
- [ ] Dedicated Entra application approved for inventory (if used)
- [ ] App registration is single-tenant and organization-owned
- [ ] Delegated `ResourceQuery.Resources.Read` consented
- [ ] Imported connector redirect URI registered as Web
- [ ] Connector operation returns HTTP 200
- [ ] `cat_ppinventory` saved and the separate Save changes confirmation completed
- [ ] Reference reopened to verify the selected connection persisted
- [ ] Flow checker shows no errors and query uses the SkipToken dynamic-content variable
- [ ] Inventory connector credential owner and rotation date recorded
- [ ] UX Agent Project support decision recorded
- [ ] Licensed non-admin tester identified

## Import

- [ ] Release downloaded from GitHub
- [ ] SHA-256 verified
- [ ] Solution imported successfully
- [ ] Version confirmed as 1.0.0.7
- [ ] Parent agent instructions visible in Copilot Studio after import; if missing, restore from source configuration in the designer before testing or sharing
- [ ] KB-01, KB-02, and KB-03 confirmed absent from the solution ZIP; retrieve the repository templates for target setup
- [ ] Import history evidence captured
- [ ] All customizations published
- [ ] Model-driven app saved and published once
- [ ] Power Platform inventory custom connector and connection reference mapped (if used)
- [ ] Real app, tenant, connection, and credential values remain outside GitHub
- [ ] Daily Power Platform inventory refresh turned on only after a full non-production test
- [ ] Complete pagination and source-scoped cleanup tested (including failed retrieval and rerun)

## Knowledge

- [ ] KB-01 placeholders replaced and content approved
- [ ] KB-02 placeholders replaced and content approved
- [ ] KB-03 placeholders replaced and content approved
- [ ] No inherited placeholder SharePoint knowledge source remains after an unmanaged upgrade
- [ ] Sources uploaded independently or connected to approved SharePoint
- [ ] Source names and descriptions aligned to scope
- [ ] KB-01 independent retrieval passed
- [ ] KB-02 independent retrieval passed
- [ ] KB-03 independent retrieval passed
- [ ] Employee channel remains disabled until approved knowledge and least-privilege security tests pass
- [ ] Intended-user permission test passed
- [ ] Review dates recorded

## Dataverse MCP

- [ ] Correct `shared_commondataserviceforapps` connection selected
- [ ] Least-privilege table permissions assigned
- [ ] Agent execution identity and shared-account permissions reviewed against restricted inventory
- [ ] Read operation passed
- [ ] Search operation passed
- [ ] Describe operation passed
- [ ] TEST create operation passed after confirmation
- [ ] Created record read back successfully
- [ ] No HTTP 403 remains

## Teams

- [ ] Approved destination recorded
- [ ] Explicit recipient configured
- [ ] Target-native action created when required
- [ ] Destination owner approved the test
- [ ] TEST message reached only the approved destination
- [ ] Received body matched the approved pattern
- [ ] Deterministic message control implemented when required

## Application and security

- [ ] Dashboard opens
- [ ] Agent Catalogue navigation works
- [ ] Agent Intake Request navigation works
- [ ] Views, forms, search, and filters work
- [ ] Tenant Agent Inventory navigation works
- [ ] Power Platform Agents view shows source-specific rows and useful publication/environment columns
- [ ] Inventory record main form shows source, platform, publication, quarantine, publisher (if supplied), environment and last seen
- [ ] Active, Power Platform Agents, Copilot Studio, and Agent Builder views work
- [ ] Licensed non-admin intended operations pass
- [ ] Unauthorized-user access test passes
- [ ] Inventory-only draft, quarantined resource, claimed-admin listing, and approved-audience scenarios tested without unwanted disclosure
- [ ] Security-role approval recorded

## Golden path

- [ ] Reuse scenario passes
- [ ] Licensing scenario passes
- [ ] Governed intake scenario passes
- [ ] Confirmation occurs before create
- [ ] Created TEST record contains intended values
- [ ] No unrequested notification is sent
- [ ] Approved channel test passes
- [ ] Evaluation thresholds pass
- [ ] First inventory refresh count matches the complete connector result
- [ ] Second inventory refresh succeeds with no duplicate Resource IDs
- [ ] Failed refresh test preserves the prior cache

## Operational handoff

- [ ] Support route documented
- [ ] Connection renewal owner documented
- [ ] Capacity monitoring configured
- [ ] Access-review schedule documented
- [ ] Knowledge-review schedule documented
- [ ] Incident and escalation route documented
- [ ] Backup and rollback approach documented
- [ ] Known limitations accepted
- [ ] Business acceptance owner approves deployment
