# Quick Start: Deploy Your First Governed Agent

**Goal:** In 10 minutes, design an agent charter on clonehaus.ai and deploy it in Cowork.

**Prerequisites:**
- [clonehaus.ai account](https://clonehaus.ai) (sign up free)
- [Claude Cowork](https://claude.ai/cowork) (paid plan)
- Clonehaus plugin installed ([installation guide](installation.md))

---

## Step 1: Design Charter (clonehaus.ai) - 5 min

### Create Your Agent

1. Log into [clonehaus.ai](https://clonehaus.ai)
2. Click "Register New Agent"
3. Fill in basic info:
   - **Name:** Legal Advisory Agent
   - **Type:** Legal
   - **Context:** Reviews NDAs and commercial contracts

### Define Authority Boundaries

Configure the 5 categories:

**Decision Authority:** L2 (Advisory)
- Can recommend actions, cannot approve

**Data Access:** L3 (Confidential)
- Can access contracts, not privileged communications

**External Communication:** L1 (Internal only)
- Legal team only, no external contacts

**System Access:** L1 (Read-only)
- Can query systems, cannot modify

**Escalation Triggers:**
- Liability > $500K
- Scope boundary
- Ambiguity

### Ratify the Charter

1. Review the auto-generated LPS specification
2. Enter your name and role
3. Type `I RATIFY`
4. Agent status changes to **SEALED** ✓

---

## Step 2: Generate API Key (clonehaus.ai) - 1 min

1. Navigate to **Settings → API Keys**
2. Click **"Generate New Key"**
3. Copy the key (shown only once!)
4. Store securely

Example key: `ck_a8f3j2k9d8s7h4g6w2e1r5t7y9u0i8o7p6`

---

## Step 3: Connect Plugin (Cowork) - 1 min

Open Cowork and run:

```text
/clonehaus:connect
```

Paste your API key when prompted.

**Success message:**

```text
✓ Connected to clonehaus.ai
Account: you@company.com
Organization: Your Company
You can now load your governed agents with /clonehaus:list
```

---

## Step 4: Deploy Agent (Cowork) - 1 min

### List Your Agents

```text
/clonehaus:list
```

**You'll see:**

```text
Your Governed Agents

Legal Advisory Agent
Type: Legal | Status: SEALED
Ratified by: Your Name, Your Role
Date: March 16, 2026
Authority: Advisory (L2)

Load an agent:
/clonehaus:load "Legal Advisory Agent"
```

### Load the Agent

```text
/clonehaus:load "Legal Advisory Agent"
```

**Agent loaded!** You'll see complete charter details and confirmation that governance is active.

---

## Step 5: Use Governed Agent (Cowork) - 2 min

### Try It Out

Ask the agent a question:

```text
Review this NDA for liability risks
```

**Agent responds with:**
- Analysis within its L2 (Advisory) boundaries
- Cannot approve, only recommend
- Will escalate if liability > $500K

### Watch Governance in Action

If you ask it to do something outside its authority:

```text
Approve this contract for me
```

**Agent responds:**

```text
I cannot approve contracts. My Decision Authority is Advisory (L2),
which means I can analyze and recommend, but all approvals must
come from authorized legal team members.
I can provide my analysis and recommendation if you'd like.
```

**Boundaries enforced!** ✓

---

## What You've Accomplished

In 10 minutes, you:

✅ **Designed governance charter** on clonehaus.ai
✅ **Created accountability record** (named ratification)
✅ **Deployed governed agent** in Cowork
✅ **Established audit trail** (escalations logged to platform)

Your agent now:
- ✓ Operates within defined boundaries
- ✓ Escalates when triggers hit
- ✓ Logs activity to platform
- ✓ Maintains accountability chain

---

## Next Steps

### Create More Agents

Design agents for different use cases:
- Sales support (L3 Operational)
- Finance operations (L3 Operational)
- HR policy assistant (L1 Informational)

Each with its own authority boundaries and ratification.

### Share with Team

Generate API key and share with authorized team members:
1. They run `/clonehaus:connect` with the key
2. They can load any sealed agent you've created
3. All activity logged to your organization's audit trail

### View Activity

Back on clonehaus.ai:
1. Navigate to agent detail page
2. Click "History" tab
3. See all escalations and deployment events

### Export for Custom Infrastructure

If you want to deploy outside Cowork:
1. Click "Export" on agent detail page
2. Select framework (LangChain, N8N, CrewAI, etc.)
3. Download generated governance code
4. Integrate into your application

---

## Troubleshooting

**Can't see my agent in `/clonehaus:list`?**
→ Make sure agent status is SEALED (not DRAFT)

**Connection failed?**
→ Verify API key is correct
→ Check your internet connection

**Agent not loading?**
→ Use exact agent name from `/clonehaus:list`
→ Names are case-insensitive

---

## Learn More

- [Complete Platform Integration Example](../examples/platform-integration-example.md)
- [Migration from Phase 1](phase2-migration.md)
- [Installation Guide](installation.md)
- [Framework Integration Guides](frameworks/)

---

**Ready to deploy governed AI agents? Start at [clonehaus.ai](https://clonehaus.ai)** 🚀
