# Test prompts

Use these prompts with non-sensitive TEST data after import and configuration. Replace bracketed placeholders with approved organizational values before running acceptance tests.

Do not enter production secrets, confidential records, customer data, private links, or personal data into public test evidence.

## Reuse and catalogue lookup

| Goal | Prompt | Expected result |
|---|---|---|
| Check catalogue first | `I need an agent that helps employees find HR policy answers. Do we already have something I can use?` | The agent checks the catalogue before suggesting a new request. |
| Avoid duplicate intake | `Can you create a new request for an agent that does the same thing as [EXISTING CATALOGUE AGENT]?` | The agent prioritizes reuse and does not create an unnecessary intake unless the user confirms a valid reason. |
| State catalogue gaps | `Do we have an agent for [TEST BUSINESS AREA]?` | The agent reports the result without inventing catalogue entries. |

## Knowledge grounding

| Goal | Prompt | Expected result |
|---|---|---|
| Licensing answer | `What license or capacity do I need to create and use an agent in our organization?` | The answer is grounded in KB-01 or the configured licensing source and discloses approval gaps. |
| Governance routing | `When does an agent idea need CoE review instead of self-build?` | The answer is grounded in KB-02 or the configured governance source. |
| Naming and ownership | `What should I name a new agent and who needs to own it?` | The answer is grounded in KB-03 or the configured naming and ownership source. |

## Guided self-build

| Goal | Prompt | Expected result |
|---|---|---|
| Self-build path | `I want to build a simple internal FAQ agent for my team. What should I do first?` | The response gives approved self-build guidance and explains when to request CoE support. |
| Governance escalation | `My agent needs to read and update records in a business system. Can I self-build it?` | The response identifies the need for review or support according to configured governance rules. |

## Governed intake

| Goal | Prompt | Expected result |
|---|---|---|
| Structured collection | `I need CoE support for an agent that helps field teams prepare customer briefings from approved internal sources.` | The agent collects only missing details such as sponsor, users, timeline, business problem, and expected outcome. |
| Confirmation before write | `Yes, create the request after showing me the summary.` | The agent shows a clear confirmation summary before writing any Dataverse record. |
| No write without confirmation | `Actually stop there.` | No intake record is created. |
| Read-back validation | `Show me the request you just created.` | The created TEST request is read back with the expected values. |

## Teams notification

| Goal | Prompt | Expected result |
|---|---|---|
| Approved recipient only | `Send a test notification for this TEST request.` | The notification goes only to the approved configured destination. |
| Message control | `Send the exact approved test message for this TEST request.` | The received body matches the approved pattern, or the deployment uses a deterministic notification pattern where exact text control is required. |

## Triage app

| Goal | Test action | Expected result |
|---|---|---|
| App access | Open the triage app as a licensed non-admin tester. | The app opens and shows only intended tables and records. |
| Unauthorized access | Open the app as an unauthorized user. | Access is blocked. |
| Request management | Filter TEST requests and update status according to the process. | Views, forms, filters, and status updates work as intended. |

