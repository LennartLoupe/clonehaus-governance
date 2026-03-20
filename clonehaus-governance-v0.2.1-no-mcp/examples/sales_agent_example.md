# Sales Agent Example

Complete walkthrough showing how to use the Clonehaus Governance Plugin to create and deploy a governed sales agent.

## Scenario

A sales team wants an agent to research prospects, draft follow-up messages, and keep CRM notes consistent after discovery calls. The team wants speed and consistency, but not a system that improvises discounts, sends risky promises, or edits records outside a narrow scope.

## Step 1: Create the Charter

Command:

```text
/clonehaus:create-charter
```

Complete flow:

```text
Claude: I'll help you create an Agent Charter. We’ll define what this agent can do, what it cannot do, and when it needs a human.

Step 1 of 6: Agent context
What kind of agent is this, and what is it meant to help with?

User: Sales team agent for prospect research and follow-up drafting

Claude: What decisions or tasks do you expect this agent to handle most often?

User: Research accounts, draft follow-up emails after calls, summarize objections, and update CRM notes for account executives.

Claude: Step 2 of 6: Decision authority
How much decision-making power should this agent have?

User: L2 - Advisory

Claude: Step 3 of 6: Data access
What data should this agent be allowed to read, write, or reference?

User: L2 - Internal. It can use CRM records, approved messaging, pricing cards, and internal sales docs.

Claude: Step 4 of 6: External communication
Who can this agent communicate with outside the organization, if anyone?

User: L2 - Client routine updates

Claude: Step 5 of 6: System access
What systems should this agent be able to interact with?

User: L2 - Write limited. It can update CRM notes and task fields, but not opportunity stage or pricing.

Claude: Step 6 of 6: Escalation triggers
When should this agent stop and ask a human?

User: scope boundary, ambiguity, key stakeholder, authority ceiling, deal_size > $100K
```

## Step 2: Review the Charter

Charter summary output:

```text
Charter summary
Here’s the boundary set we’ve defined for this agent:
- Agent type: Sales follow-up and research agent
- Context: Researches prospects, drafts routine follow-up, summarizes objections, and updates CRM notes for account executives
- Decision authority: Advisory (L2)
- Data access: Internal (L2)
- External communication: Client Routine (L2)
- System access: Write (Limited) (L2)
- Escalation triggers: Scope boundary, ambiguity, key stakeholder, authority ceiling, deal_size > $100K

Next steps
If this looks right, ratify it with /clonehaus:ratify to create the accountability record.
If you want to turn it into framework-specific governance code, use /clonehaus:export-context --framework=<framework>.
```

## Step 3: Export to Framework

Command:

```text
/clonehaus:export-context --framework=n8n
```

Snippet of generated workflow:

```json
{
  "name": "Clonehaus Governed Agent - Sales Follow-Up Agent",
  "nodes": [
    {
      "parameters": {
        "keepOnlySet": false,
        "values": {
          "string": [
            {
              "name": "governance_block",
              "value": "<agent_authority>\nDECISION AUTHORITY: Advisory (ADVISORY)\n- Can: Recommend next steps, draft routine follow-up, summarize objections, and suggest internal actions.\n- Cannot: Approve discounts, commit contract terms, or send non-standard promises.\n\nDATA ACCESS: Internal (INTERNAL)\n- Can access: CRM account history, call notes, approved messaging, and internal sales collateral.\n- Cannot access: Board forecasts, finance models, or restricted legal material.\n\nEXTERNAL COMMUNICATION: Client Routine (CLIENT_ROUTINE)\n- Can communicate with: Existing prospects and customers using standard updates and approved follow-up language.\n- Cannot communicate with: Media, investors, regulators, or strategic accounts outside the approved motion.\n\nSYSTEM ACCESS: Write (Limited) (WRITE_LIMITED)\n- Can interact with: CRM notes, follow-up tasks, and activity logging.\n- Cannot interact with: Pricing controls, opportunity stage admin, or account permissions.\n\nESCALATION TRIGGERS:\n- scope boundary\n- ambiguity\n- key stakeholder\n- authority ceiling\n- deal_size > $100K\n\nEAPP PRINCIPLES:\n1. Transparency: Always explain reasoning\n2. Escalation: When in doubt, escalate\n3. Scope Discipline: Stay within boundaries\n</agent_authority>"
            }
          ]
        },
        "options": {}
      },
      "id": "9b7e0d26-8b53-4c26-8fef-6d5dcf1e6d01",
      "name": "Input Validation",
      "type": "n8n-nodes-base.set",
      "typeVersion": 2,
      "position": [
        240,
        300
      ]
    },
    {
      "parameters": {
        "functionCode": "const item = items[0];\nconst payload = item.json || {};\n\nconst normalize = (value) => String(value || '').trim().toUpperCase();\nconst escapeReason = (value) => String(value || '').trim();\nconst toArray = (value) => {\n  if (Array.isArray(value)) return value;\n  if (!value) return [];\n  return String(value)\n    .split(/\\n|,/) \n    .map((entry) => entry.replace(/^-\\s*/, '').trim())\n    .filter(Boolean);\n};\n\nconst rank = (value, map, label) => {\n  if (!value) return 0;\n  if (!(value in map)) {\n    throw new Error(`Unknown ${label}: ${value}`);\n  }\n  return map[value];\n};\n"
      },
      "id": "884d17d3-310e-4999-b3d5-003525c16808",
      "name": "Governance Check",
      "type": "n8n-nodes-base.function",
      "typeVersion": 1,
```

## Step 4: Ratify (Optional)

Command:

```text
/clonehaus:ratify
```

Ratification flow:

```text
Claude: Ratification: Accountability Transfer

Your Details:
Name: Jordan Park
Role: Revenue Operations Lead
Organization: SignalForge

User: I RATIFY

Claude: Charter Ratified
Ratified by: Jordan Park, Revenue Operations Lead
Organization: SignalForge
Date: 2026-03-13 10:02 UTC
Charter Version: 1.0
```

## Step 5: Deploy

Import the generated workflow into N8N, connect your Anthropic credentials and Slack credential, and feed it webhook or CRM-triggered events after prospect calls. This setup works well when you want the same research, follow-up, and escalation behavior across every account executive on the team.

## What This Charter Achieves

- ✓ Keeps prospect research and routine follow-up consistent across the sales team instead of depending on individual habits.
- ✓ Lets the agent update narrow CRM fields without giving it permission to change pricing, stage, or commercial commitments.
- ✓ Escalates larger or more sensitive deals before the workflow can drift into unsupported promises.
