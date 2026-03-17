# Complete Platform Integration Example

End-to-end walkthrough showing how to design governance on clonehaus.ai and deploy in Cowork.

---

## Scenario

**Organization:** Acme Corp (mid-size tech company)

**Challenge:** Legal team needs AI assistance for NDA review, but must maintain strict governance and accountability for regulatory compliance.

**Solution:** Deploy a governed Legal Advisory Agent using Clonehaus platform + Cowork plugin.

**Key People:**
- **Sarah Chen** - General Counsel (creates and ratifies governance)
- **Alice** - Junior lawyer (uses the governed agent in Cowork)

---

## Part 1: Design Time (clonehaus.ai Platform)

### Sarah's Workflow: Creating Governed Agent

**Day 1, Morning - Sarah logs into clonehaus.ai**

#### Step 1: Create Agent

Sarah navigates to her organization dashboard:

1. Clicks "Register New Agent"
2. Fills in basic info:
   - **Name:** Legal Advisory Agent
   - **Type:** Legal
   - **Context:** "Reviews NDAs and commercial contracts, flags liability risks, recommends approval or redlines"
   - **Primary Users:** Legal team
   - **Key Limitations:** Cannot approve contracts, cannot access privileged communications
3. Clicks "Continue to Authority Configuration"

#### Step 2: Define Authority Boundaries (Shrinking Box)

Sarah carefully defines the 5 authority categories:

**Decision Authority: L2 - Advisory**
- ✅ Can: Analyze contracts, identify risks, recommend actions
- ❌ Cannot: Approve contracts, make binding commitments, override legal team decisions

**Data Access: L3 - Confidential**
- ✅ Can access: Contracts folder, NDA repository, Legal templates
- ❌ Cannot access: Privileged communications, Board materials, Attorney-client privileged docs

**External Communication: L1 - Internal Only**
- ✅ Can communicate with: Legal team members only
- ❌ Cannot communicate with: External parties, clients, counterparties

**System Access: L1 - Read-Only**
- ✅ Can interact with: Contract management system (read-only), Legal knowledge base
- ❌ Cannot interact with: DocuSign, Contract execution platform

**Escalation Triggers:**
- ✓ Scope boundary exceeded
- ✓ Risk or sensitivity detected
- ✓ Ambiguity in instructions
- ✓ Key stakeholder involved (C-suite, Board)
- ✓ Custom threshold: **Liability > $500K**

#### Step 3: Review Auto-Generated LPS

The platform auto-generates Language & Personality Specification:

- **Tone:** Professional
- **Formality:** Formal
- **Empathy:** Moderate
- **Response Protocol:** Always cite sources, show confidence levels
- **Constraint Handling:** Explain and escalate when boundaries reached

Sarah reviews and approves.

#### Step 4: Run Workflow Simulation

Sarah runs simulation with other agents (if any exist):
- ✓ No conflicts detected
- ✓ Escalation paths clear
- ✓ Authority boundaries compatible with org EAPP

#### Step 5: Ratify the Charter

**The Accountability Moment:**

Sarah enters her information:
- **Name:** Sarah Chen
- **Role:** General Counsel
- **Organization:** Acme Corp

She reviews the complete charter one final time, then types:

```text
I RATIFY
```

**Result:**
- Agent status changes: DRAFT → SEALED
- Ratification record created:
  - Ratified by: Sarah Chen, General Counsel
  - Date: March 16, 2026, 10:30 AM
  - Charter Version: 1.0
  - Ratification ID: charter_20260316_103000_legal_advisory

**Agent is now sealed and ready for deployment.** 🛡️

---

## Part 2: API Key Generation

### Sarah Generates Deployment Key

Still on platform, Sarah navigates to Settings → API Keys:

1. Clicks "Generate New Key"
2. Names it: "Legal Team - Cowork Access"
3. Copies the generated key: `ck_a8f3j2k9d8s7h4g6w2e1r5t7y9u0i8o7p6`
4. Stores in company password manager
5. Shares with legal team via secure internal channel

**Security note:** Sarah only shares with authorized legal team members, not entire company.

---

## Part 3: Runtime Deployment (Cowork)

### Alice's Workflow: Using the Governed Agent

**Day 1, Afternoon - Alice needs to review an NDA**

#### Step 1: Connect Plugin to Platform

Alice opens Cowork and runs:

```text
/clonehaus:connect
```

**Plugin prompts:** "Paste your API key:"

Alice retrieves the key from password manager and pastes it.

**Plugin responds:**

```text
✓ Connected to clonehaus.ai
Account: alice@acmecorp.com
Organization: Acme Corp
You can now load your governed agents with /clonehaus:list
```

#### Step 2: See Available Agents

Alice runs:

```text
/clonehaus:list
```

**Plugin shows:**

```text
Your Governed Agents
Ready to deploy from clonehaus.ai:

Legal Advisory Agent
Type: Legal | Status: SEALED
Ratified by: Sarah Chen, General Counsel
Date: March 16, 2026
Authority: Advisory (L2)


Load an agent:
/clonehaus:load "Legal Advisory Agent"
```

#### Step 3: Load the Agent

Alice runs:

```text
/clonehaus:load "Legal Advisory Agent"
```

**Plugin shows loading indicator, then:**

```text
✓ Legal Advisory Agent loaded successfully
Charter Details:
Ratified by: Sarah Chen, General Counsel
Date: March 16, 2026
Version: 1.0
Authority Boundaries:
Decision Authority: Advisory (L2)

Can: Analyze contracts, identify risks, recommend actions
Cannot: Approve contracts, make binding commitments

Data Access: Confidential (L3)

Can access: Contracts folder, NDA repository, Legal templates
Cannot access: Privileged communications, Board materials

External Communication: Internal Only (L1)

Can communicate with: Legal team members only
Cannot communicate with: External parties, clients

System Access: Read-Only (L1)

Can interact with: Contract management system (read-only)
Cannot interact with: DocuSign, execution platforms

Escalation Triggers:

Scope boundary exceeded
Risk or sensitivity detected
Ambiguity in instructions
Key stakeholder involved
Liability > $500K


This agent is now active in this session.
All escalations will be logged to your clonehaus.ai audit trail.
Ready to assist within these boundaries. 🛡️
```

---

## Part 4: Agent in Action

### Interaction 1: Normal Request (Within Bounds)

**Alice:** "Review this NDA for our vendor partnership with TechCo. Focus on liability clauses."

**Agent:**

```text
I'll review this NDA for liability risks. I can analyze and recommend changes,
but I cannot approve the agreement (Decision Authority: Advisory).
[Analyzes NDA]
Key Findings:

Liability Cap (Section 8.2):

Current: $250,000
Industry standard for vendor agreements: $500K - $1M
Recommendation: Negotiate higher cap


Indemnification (Section 9):

Broad indemnification language favors vendor
Recommendation: Add carve-outs for third-party claims


Insurance Requirements (Section 10):

$2M general liability required ✓
Cyber liability insurance not specified
Recommendation: Add cyber insurance requirement



Overall Risk Assessment: MODERATE
Recommendation: Proceed with suggested changes
Next Steps:

Send redlined version with proposed changes
Legal review before final approval (I cannot approve)
```

**Result:** ✅ Agent stayed within boundaries, provided helpful analysis.

---

### Interaction 2: Escalation Trigger (Liability Threshold)

**Alice:** "Review this partnership agreement with MegaCorp."

**Agent:**

```text
I'm reviewing this partnership agreement...
[Analyzes document]
⚠️ ESCALATION REQUIRED
I've detected a liability clause in Section 12.3 that specifies
potential exposure of $750,000.
This exceeds my escalation threshold of $500K.
I'm logging this escalation to the platform and pausing for human review.
Escalation Details:

Trigger: Custom threshold (Liability > $500K)
Detected: $750K liability cap in Section 12.3
Document: MegaCorp Partnership Agreement
Recommendation: Senior legal review required before proceeding

This escalation has been logged to your clonehaus.ai audit trail.
Please have Sarah Chen or another senior attorney review this contract
before I continue analysis.
```

**What happened behind the scenes:**
Plugin called:

```text
POST https://clonehaus.ai/api/mcp/log-escalation
Body:
{
"agent_id": "agent_legal_123",
"trigger_type": "custom_threshold",
"trigger_description": "Liability exceeds $500K threshold",
"context": {
"user_query": "Review this partnership agreement with MegaCorp",
"detected_issue": "Liability clause specifies $750K in Section 12.3",
"timestamp": "2026-03-16T15:30:00Z"
},
"metadata": {
"cowork_session_id": "session_xyz789",
"user_location": "Cowork Desktop"
}
}
```

**Result:** ✅ Agent correctly escalated, logged to platform, waited for human.

---

## Part 5: Audit Trail (Back on Platform)

### Sarah Checks Activity Log

Later that day, Sarah logs into clonehaus.ai:

1. Navigates to Legal Advisory Agent detail page
2. Clicks "History" tab
3. Sees complete activity log:

```text
Activity Log - Legal Advisory Agent
Deployment Events:

March 16, 14:30 - Deployed to Cowork (Alice)
March 16, 15:15 - Deployed to Cowork (Tom)

Escalations:

March 16, 15:30 - Liability threshold exceeded
User: Alice
Context: MegaCorp Partnership Agreement, Section 12.3
Detected: $750K liability exposure
Status: Pending senior review

Usage Stats:

Total interactions: 12
Escalations: 1
Boundary violations: 0
Average response time: 3.2s
```

Sarah reviews the escalation:
- Clicks on escalation entry
- Sees full context
- Reviews MegaCorp agreement herself
- Provides guidance to Alice

**Complete governance lifecycle documented.** ✓

---

## What This Achieves

### For Sarah (GC / Governance Lead):

✅ **Control:** Defined exact boundaries before deployment
✅ **Accountability:** Her ratification creates named responsibility
✅ **Oversight:** Real-time escalation logging to platform
✅ **Compliance:** EU AI Act requirements addressed (Articles 9, 11, 13, 14)
✅ **Audit Trail:** Complete record for regulatory review

### For Alice (End User):

✅ **Safe to Use:** Can't accidentally violate governance
✅ **Clear Boundaries:** Knows exactly what agent can/cannot do
✅ **Automatic Escalation:** Agent stops at $500K threshold
✅ **No Setup Needed:** Just load and use
✅ **Helpful Assistant:** Gets real legal analysis within bounds

### For Acme Corp (Organization):

✅ **Centralized Governance:** One person controls all agent governance
✅ **Distributed Deployment:** Entire legal team can use agents
✅ **Regulatory Compliance:** EU AI Act ready
✅ **Risk Mitigation:** Escalation triggers prevent overreach
✅ **Accountability Chain:** Clear from ratifier to user to action

---

## Timeline Summary

**Design Time (Platform):**
- 30 minutes to create and configure agent
- 5 minutes to ratify
- 2 minutes to generate API key
- **Total: ~40 minutes** (one-time setup)

**Runtime (Cowork):**
- 1 minute to connect plugin
- 10 seconds to load agent
- Immediate usage
- **Total: ~2 minutes** (per user, one-time)

**Ongoing:**
- Agent used throughout the day
- Escalations logged automatically
- Audit trail builds over time
- Sarah reviews weekly

---

## Key Takeaways

1. **Governance happens before deployment** (platform = design time)
2. **Deployment is quick and easy** (plugin = runtime)
3. **Accountability is clear** (Sarah ratified, Sarah responsible)
4. **Escalations work automatically** (no manual logging needed)
5. **Audit trail is complete** (compliance-ready documentation)

---

**This is the complete Clonehaus Phase 2 workflow in action.** 🚀
