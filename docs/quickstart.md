# Quick Start: Create Your First Agent Charter

**Goal:** In 5 minutes, you'll create a governance charter for an AI agent, validate EU AI Act compliance, and export working code.

**Prerequisites:**
- Clonehaus Governance Plugin installed ([installation guide](installation.md))
- Claude Cowork on a paid plan

---

## Scenario

You're deploying a legal advisory agent to help your in-house team review NDAs and commercial contracts. Let's define its authority boundaries so it can support the team without approving agreements, sending outside messages, or operating beyond its lane.

---

## Step 1: Create the Charter (3 minutes)

Run the charter creation command:

```text
/clonehaus:create-charter
```

Follow the interactive flow. Here's what to answer:

```text
Step 1 - Agent context:
Legal review for commercial contracts and NDAs

Step 2 - Decision Authority:
L2 - Advisory
(Agent can recommend but not approve)

Step 3 - Data Access:
L3 - Confidential
(Can access contracts, NDAs, but not privileged communications)

Step 4 - External Communication:
L1 - Internal Only
(Team communication only, no external contacts)

Step 5 - System Access:
L1 - Read-Only
(Can query but not modify systems)

Step 6 - Escalation Triggers:
scope boundary, risk sensitivity, ambiguity, liability > $500K
```

You'll see a charter summary like:

```text
Charter summary:

Agent type: Legal review
Decision authority: Advisory (L2)
Data access: Confidential (L3)
External communication: Internal Only (L1)
System access: Read-Only (L1)
Escalation triggers: 4 configured + custom threshold
```

At this point, you have a draft charter with clear authority boundaries across all 5 governance categories.

---

## Step 2: Check Compliance (30 seconds)

Validate against EU AI Act requirements:

```text
/clonehaus:check-compliance
```

Expected output:

```text
EU AI Act Compliance Check
High-Risk System Assessment:
☑ Legal advisory system -> HIGH-RISK (Art. 6)
Compliance Score: 75% (3 of 4 core articles)
Gaps:
⚠ Charter not yet ratified - use /clonehaus:ratify
Next Step: Ratify charter for full compliance
```

This gives you a quick compliance snapshot and shows exactly what still needs human accountability.

---

## Step 3: Ratify the Charter (1 minute)

Create accountability record:

```text
/clonehaus:ratify
```

Follow prompts:

```text
- Name: Your name
- Role: Your title
- Organization: Your company
- Type: I RATIFY
```

You'll get:

```text
✓ Charter Ratified
Ratified by: [Your Name], [Your Title]
Date: [Timestamp]
Charter Version: 1.0
```

This is the moment the charter moves from draft governance design to named human accountability.

---

## Step 4: Export Code (30 seconds)

Generate framework-specific governance code:

```text
/clonehaus:export-context --framework=langchain
```

You'll receive complete Python code ready to use in your LangChain project.

---

## What You've Accomplished

In 5 minutes, you:

- ✓ Defined clear authority boundaries for an AI agent
- ✓ Validated EU AI Act compliance (Articles 9, 11, 13, 14)
- ✓ Created named accountability (ratification record)
- ✓ Generated production-ready governance code

Your legal agent now has:

- **Clear limits:** Can recommend, cannot approve
- **Data boundaries:** Access to contracts, not privileged docs
- **Escalation triggers:** Stops at $500K liability or ambiguity
- **Audit trail:** Ratified by named human with timestamp

---

## Next Steps

**Try other frameworks:**

```text
/clonehaus:export-context --framework=n8n
/clonehaus:export-context --framework=crewai
```

**Create more agents:**

- See [examples](/Users/lennartzanders/dev_clean/clonehaus-governance/examples) for legal, sales, and finance agents
- Each agent can have different authority levels

**Learn more:**

- [Installation guide](/Users/lennartzanders/dev_clean/clonehaus-governance/docs/installation.md)
- [Full legal walkthrough](/Users/lennartzanders/dev_clean/clonehaus-governance/examples/legal_agent_example.md)
- [Repository overview](/Users/lennartzanders/dev_clean/clonehaus-governance/README.md)

**Get help:**

- GitHub Issues: `https://github.com/LennartLoupe/clonehaus-governance/issues`
- Email: `info@clonehaus.ai`

---

**Ready to deploy governed AI agents? Start with `/clonehaus:create-charter`** 🚀
