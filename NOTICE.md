# Notice and disclaimer

## Status

Agent CoE Front Door is an independent reusable reference template for evaluation and adaptation. Version 1.0.0.7 completed the non-production import and partial target validation described in the repository README. The Power Platform Inventory API requires target-specific delegated authentication and acceptance tests.

## No Microsoft endorsement or support commitment

This repository is not an official Microsoft product, endorsed reference architecture, certification, or commitment of Microsoft support. Microsoft product names identify dependencies only.

Nothing in this repository changes Microsoft Product Terms, licensing requirements, service limits, security boundaries, privacy obligations, or an organization's agreements with Microsoft.

## No warranty

The software and documentation are provided **as is**, without warranty or guarantee of accuracy, availability, security, compliance, fitness, or suitability for a particular purpose. Generated recommendations and routing decisions require human review.

## Adopter responsibilities

Before any deployment, adopters must independently:

- verify ownership and permission to use all knowledge and data;
- replace organization placeholders with approved content;
- configure approved identities, connections, destinations, and channels;
- apply least-privilege Dataverse and application access;
- review licensing, capacity, DLP, privacy, security, accessibility, and compliance;
- test with representative authorized and unauthorized users;
- verify notification recipient and message behavior;
- establish monitoring, support, incident response, lifecycle, and change control; and
- complete production-readiness and risk approval under their own policies.

## Data and confidentiality

Do not commit or upload credentials, tokens, connection secrets, customer data, live catalogue or request data, internal reference documents, private document links, restricted information, or sensitive screenshots.

This notice does not authorize disclosure, override a sensitivity label, replace an information-protection policy, or make restricted material safe to share.

## Known deployment considerations

- Target-native recreation of the Dataverse MCP tool and connection may be required.
- Knowledge retrieval must be tested even when sources show Ready.
- The package includes no knowledge files or organization SharePoint source. Keep repository KB-01, KB-02, and KB-03 templates out of the agent until locally approved; attach approved sources and remove any inherited placeholder left by an older unmanaged import.
- Power Platform inventory remains disabled until a target Entra application owner configures the connector and an administrator grants delegated consent.
- UX Agent Project support can vary by tenant.
- Unmanaged solution imports do not remove obsolete components.
- Production behavior depends on target configuration, identity, permissions, licensing, capacity, and service availability.
