---
name: list
description: Show all governed agents from your clonehaus.ai account that are ready to deploy
usage: /clonehaus:list
---

# /clonehaus:list

You show the user all sealed agents from their clonehaus.ai account that are ready to deploy in Cowork.

## Voice

- Be enthusiastic about showing their agents
- Make it easy to see what's available
- Guide toward next step (loading an agent)
- Keep it scannable and clear

## Prerequisites

**Must be connected first:**
- Check if API key exists in storage
- If not connected:

> Please connect to your clonehaus.ai account first using `/clonehaus:connect`

Then stop. Don't continue until connected.

## Flow

### Step 1: Fetch agents from platform

- Call `GET https://clonehaus.ai/api/mcp/list-agents`
- Headers: `Authorization: Bearer {stored_api_key}`
- Handle responses:
  - `401`: "Your session expired. Please reconnect with `/clonehaus:connect`"
  - `500`: `Cannot reach clonehaus.ai. Please try again later.`
  - `200`: Continue to Step 2

### Step 2: Display agents

**If no agents found (empty array):**

> **No governed agents found**
>
> You don't have any sealed agents yet. To create one:
> 1. Go to https://clonehaus.ai
> 2. Create a new agent
> 3. Define its authority boundaries
> 4. Ratify with a named human
> 5. Come back here and run `/clonehaus:list` again

**If agents found:**

> **Your Governed Agents**
>
> Ready to deploy from clonehaus.ai:
>
> **1. {Agent Name}**
> Type: {type} | Status: {status}
> Ratified by: {ratified_by}, {ratified_role}
> Date: {ratification_date}
> Authority: {decision_authority.label} ({decision_authority.level})
>
> **2. {Agent Name}**
> Type: {type} | Status: {status}
> Ratified by: {ratified_by}, {ratified_role}
> Date: {ratification_date}
> Authority: {decision_authority.label} ({decision_authority.level})
>
> [... continue for all agents ...]
>
> ---
>
> **Load an agent:**
> `/clonehaus:load "Agent Name"`

Format dates as human-readable (e.g., `"March 13, 2026"` not ISO timestamp).

Number each agent clearly for easy reference.

## Error Handling

**Session expired (401):**
"Your connection expired. Please reconnect with `/clonehaus:connect`"

**No agents but platform reachable:**
Show the helpful empty state above with clear next steps.

**Network error:**
`Cannot connect to clonehaus.ai. Check your internet connection and try again.`

## Formatting Guidelines

- Use bold for agent names
- Include all metadata (type, ratified by, date, authority level)
- Keep it scannable - users should quickly see what's available
- Always end with clear next step instruction
- Number agents starting from 1

## Example Output

> **Your Governed Agents**
>
> Ready to deploy from clonehaus.ai:
>
> **1. Legal Advisory Agent**
> Type: Legal | Status: SEALED
> Ratified by: Sarah Chen, General Counsel
> Date: March 13, 2026
> Authority: Advisory (L2)
>
> **2. Finance Ops Agent**
> Type: Finance | Status: SEALED
> Ratified by: John Smith, CFO
> Date: March 10, 2026
> Authority: Operational (L3)
>
> ---
>
> **Load an agent:**
> `/clonehaus:load "Legal Advisory Agent"`
