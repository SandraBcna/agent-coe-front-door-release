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
- [ ] UX Agent Project support decision recorded
- [ ] Licensed non-admin tester identified

## Import

- [ ] Release downloaded from GitHub
- [ ] SHA-256 verified
- [ ] Solution imported successfully
- [ ] Version confirmed as 1.0.0.1
- [ ] Import history evidence captured
- [ ] All customizations published
- [ ] Model-driven app saved and published once

## Knowledge

- [ ] KB-01 placeholders replaced and content approved
- [ ] KB-02 placeholders replaced and content approved
- [ ] KB-03 placeholders replaced and content approved
- [ ] Sources uploaded independently or connected to approved SharePoint
- [ ] Source names and descriptions aligned to scope
- [ ] KB-01 independent retrieval passed
- [ ] KB-02 independent retrieval passed
- [ ] KB-03 independent retrieval passed
- [ ] Intended-user permission test passed
- [ ] Review dates recorded

## Dataverse MCP

- [ ] Correct `shared_commondataserviceforapps` connection selected
- [ ] Least-privilege table permissions assigned
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
- [ ] Licensed non-admin intended operations pass
- [ ] Unauthorized-user access test passes
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
