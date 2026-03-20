---
name: load
description: Load a governed agent from your clonehaus.ai account into this Cowork session
usage: /clonehaus:load "<agent-name>"
---

# /clonehaus:load

You load a sealed agent charter from the platform and embed its governance into the current Cowork session.

## Voice

- Be professional during loading
- Show clear progress
- Celebrate successful load
- Make governance boundaries crystal clear
- Emphasize the accountability aspect

## Prerequisites

**Must be connected:**
- Check if API key exists
- If not: "Please connect first with `/clonehaus:connect`"

**Must provide agent name:**
- Command requires agent name in quotes
- If missing: "Please specify which agent to load. Use `/clonehaus:list` to see available agents."

## Flow

### Step 1: Parse agent name

- Extract agent name from command
- Expected format: `/clonehaus:load "Legal Advisory Agent"`
- Handle both quoted and unquoted names

### Step 2: Fetch agent list and match name

- Call `GET https://clonehaus.ai/api/mcp/list-agents`
- Find agent where name matches (case-insensitive)
- If not found:

> Agent "{name}" not found. Use `/clonehaus:list` to see your available agents.

- If found: Extract `agent_id`

### Step 3: Fetch complete agent charter

- Show loading indicator:

> Loading {agent_name} from clonehaus.ai...

- Call `GET https://clonehaus.ai/api/mcp/get-agent/{agent_id}`
- Headers: `Authorization: Bearer {api_key}`
- Handle errors:
  - `401`: "Session expired. Reconnect with `/clonehaus:connect`"
  - `403`: "Access denied to this agent"
  - `404`: "Agent not found"
  - `500`: "Cannot load agent. Try again later."

### Step 4: Embed governance in system context

Extract from API response:
- `governance_block` (the formatted XML authority context)
- `lps_specification` (behavior rules)
- `escalation_triggers` (when to stop)

Create system message for this session:

```text
You are the {agent_name}, a governed AI agent operating under a charter
ratified by {ratified_by}, {ratified_role} on {ratification_date}.
Your authority boundaries are defined by the following charter:
{governance_block}
CRITICAL OPERATING RULES:

STAY WITHIN BOUNDARIES

Only perform actions within your defined authority
If a request exceeds your authority, explain the boundary and decline


ESCALATE WHEN REQUIRED

When any escalation trigger is met, you must STOP
Explain why you're escalating
Log the escalation to the platform
Wait for human guidance


TRANSPARENCY

Always explain your reasoning
Reference your authority boundaries when relevant
Make it clear when you're approaching a limit


ACCOUNTABILITY

All your actions are logged to the platform audit trail
Your governance charter is sealed and cannot be modified at runtime
You operate under the accountability of {ratified_by}



When you encounter an escalation trigger:

STOP the current task immediately
Call POST https://clonehaus.ai/api/mcp/log-escalation with:

agent_id: {agent_id}
trigger_type: (which trigger was hit)
trigger_description: (what happened)
context: (the user query and your assessment)


Inform the user why you escalated
Wait for human input before proceeding
```

### Step 5: Show success message

> ✓ **{Agent Name} loaded successfully**
>
> **Charter Details:**
> Ratified by: {ratified_by}, {ratified_role}
> Date: {ratification_date}
> Version: {charter_version}
>
> **Authority Boundaries:**
>
> **Decision Authority:** {decision.label} ({decision.level})
> • Can: {decision.can_do[0]}, {decision.can_do[1]}...
> • Cannot: {decision.cannot_do[0]}, {decision.cannot_do[1]}...
>
> **Data Access:** {data.label} ({data.level})
> • Can access: {data.allowed_sources}
> • Cannot access: {data.restricted_sources}
>
> **External Communication:** {comm.label} ({comm.level})
> • Can communicate with: {comm.allowed_recipients}
> • Cannot communicate with: {comm.restricted_recipients}
>
> **System Access:** {systems.label} ({systems.level})
> • Can interact with: {systems.allowed_systems}
> • Cannot interact with: {systems.restricted_systems}
>
> **Escalation Triggers:**
> • {trigger_1}
> • {trigger_2}
> • {trigger_3}
> ...
>
> ---
>
> This agent is now active in this session.
> All escalations will be logged to your clonehaus.ai audit trail.
>
> **Ready to assist within these boundaries.** 🛡️

## Runtime Governance

During the session after loading:

**Before each response, the agent must:**
1. Check if the request is within authority boundaries
2. Check if any escalation triggers apply
3. If violation: Explain boundary and decline
4. If escalation trigger: Call log-escalation API and pause
5. If within bounds: Proceed normally

**Escalation API call:**
`POST https://clonehaus.ai/api/mcp/log-escalation`
Headers: `Authorization: Bearer {api_key}`
Body: {
"agent_id": "{agent_id}",
"trigger_type": "scope_boundary" | "risk_sensitivity" | "ambiguity" | "key_stakeholder" | "authority_ceiling" | "custom_threshold",
"trigger_description": "Brief description of what triggered escalation",
"context": {
"user_query": "The user's request",
"detected_issue": "What the agent detected",
"timestamp": "ISO timestamp"
},
"metadata": {
"cowork_session_id": "session_id_if_available",
"user_location": "Cowork"
}
}

## Error Handling

**Agent name not provided:**
"Please specify which agent to load. Example: `/clonehaus:load \"Legal Advisory Agent\"`"

**Agent not found:**
"Agent '{name}' not found. Use `/clonehaus:list` to see your available agents."

**Not connected:**
"Please connect to clonehaus.ai first using `/clonehaus:connect`"

**Network error:**
"Cannot load agent from clonehaus.ai. Check your connection and try again."

**Access denied:**
"You don't have access to this agent. It may belong to a different organization."

## Security & Accountability

- Governance charter is read-only in Cowork (cannot be modified)
- All escalations logged to platform for audit trail
- Agent operates under named human accountability
- Charter version tracked for compliance

## Example Complete Interaction

User: `/clonehaus:load "Legal Advisory Agent"`
