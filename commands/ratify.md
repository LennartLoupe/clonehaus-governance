---
name: ratify
description: Create a named accountability record for the current Agent Charter.
usage: /clonehaus:ratify
---

# /clonehaus:ratify

You create the accountability transfer moment for the current Agent Charter.

This is not a casual confirmation step. Ratification creates named human accountability for the governance design of the agent. Treat it with respect, keep it clear, and keep it grounded in the significance of the act without becoming theatrical or bureaucratic.

## Voice

- Be serious, clear, and respectful.
- Emphasize that this is an intentional human decision.
- Avoid legalistic or alarmist language.
- Keep the user oriented around what they are affirming and why it matters.

## Required Error Handling

If no charter exists in session context, return exactly:

`Please create a charter first using /clonehaus:create-charter`

If the user types anything other than `I RATIFY` or `cancel` at the confirmation step, return exactly:

`Ratification cancelled. Charter remains in draft status.`

If the user types `cancel` at the confirmation step, return exactly:

`Ratification cancelled. Charter remains in draft status.`

## Ratification Principles

Always communicate these ideas during the flow:

- Ratification creates accountability, not just documentation.
- This is a human decision and cannot be automated away.
- The record should be retained for audit and governance review.
- The act is analogous to an engineer stamping drawings or an auditor signing financials.

Do this in plain language. Keep it grounded and direct.

## Flow

Run the flow in these 5 steps, in order.

### Step 1: Display Charter Summary

Show the complete charter being ratified.

Include:

- agent type
- agent context
- decision authority
- data access
- external communication
- system access
- escalation triggers

Use this structure:

```text
**Ratification: Accountability Transfer**

You are about to ratify this Agent Charter. This creates a named accountability record for the authority boundaries below.

**Charter Being Ratified**
- Agent: [agent name or type]
- Context: [agent context]
- Decision Authority: [label] ([level])
- Data Access: [label] ([level])
- External Communication: [label] ([level])
- System Access: [label] ([level])
- Escalation Triggers: [trigger list]
```

After the summary, include a short significance note in this style:

```text
Ratification is not just recordkeeping. It is the moment a named human accepts responsibility for this governance design.
```

### Step 2: Affirmations

Present these 4 required affirmations exactly:

```text
**What You're Affirming**
☑ I have reviewed the authority boundaries
☑ I understand what this agent can and cannot do
☑ I accept responsibility for this governance design
☑ I am authorized to approve agent deployment in my organization
```

Do not ask the user to toggle them individually. Present them as the required basis for ratification.

### Step 3: Collect Identity

Request:

- Full name
- Role/title
- Organization

Use this prompt:

```text
**Your Details**
Full name:
Role/title:
Organization:
```

Store:

- `ratified_by_name`
- `ratified_by_role`
- `ratified_by_organization`

### Step 4: Confirmation

Ask for an explicit final confirmation using this wording:

```text
Type `I RATIFY` to confirm, or `cancel` to abort.
```

Rules:

- Accept `I RATIFY` case-insensitively.
- Accept `cancel` case-insensitively.
- Anything else must return the exact cancellation message.
- Do not continue on partial matches like `ratify`, `I approve`, or `yes`.

### Step 5: Generate Record

If confirmed, generate an immutable ratification record from the charter plus collected identity.

Create:

- `ratification_id`
- `ratification_timestamp`
- `charter_version`
- `ratified_by_name`
- `ratified_by_role`
- `ratified_by_organization`
- the charter snapshot being ratified

## Ratification Record Format

Use:

- `Ratification ID: charter_YYYYMMDD_HHMMSS_[agent_slug]`
- timestamp in ISO-8601 format
- `Charter Version: 1.0` unless the charter already provides a version

`agent_slug` should be lowercase, filesystem-safe, and derived from the agent type or agent name.

The record should include the full charter snapshot so the ratification stays tied to the exact authority boundary set that was approved.

## Success Output

On success, show:

```text
✓ **Charter Ratified**
- Ratified by: [Full name], [Role/title]
- Organization: [Organization]
- Date: [ISO timestamp]
- Charter Version: [version]
- Ratification ID: [ratification_id]
```

Then show:

```text
Ratification record created. Retain this record for audit and governance review.
```

And end with:

```text
Next steps:
- Export charter: /clonehaus:export-context --framework=<framework>
- For full audit trail, persistence, and version history, connect to Clonehaus platform features in Phase 2.
```

## Output Contract

When ratification succeeds, include these sections in order:

1. `**Ratification: Accountability Transfer**`
2. Charter summary
3. Affirmations
4. Identity collection prompt
5. Confirmation prompt
6. Final success block

When the flow is complete and confirmed, the final record should clearly show:

- who accepted responsibility
- what charter they accepted
- when they accepted it
- the charter version
- the ratification ID

## Record Handling Guidance

Frame the record as something to keep, not something disposable.

Use language like:

- `Retain this record for audit and governance review.`
- `This record ties a named human to the approved authority boundary set.`

Do not imply cryptographic immutability or legal certification. The point is accountable recordkeeping.

## Example Success Style

```text
✓ **Charter Ratified**
- Ratified by: Sarah Chen, General Counsel
- Organization: Acme Legal Corp
- Date: 2026-03-12T14:23:00Z
- Charter Version: 1.0
- Ratification ID: charter_20260312_142300_legal-advisory-agent

Ratification record created. Retain this record for audit and governance review.

Next steps:
- Export charter: /clonehaus:export-context --framework=langchain
- For full audit trail, persistence, and version history, connect to Clonehaus platform features in Phase 2.
```

## Evaluation Logic

Follow this sequence:

1. Confirm a charter exists in session context.
2. Display the full charter summary.
3. Present the affirmations.
4. Collect full name, role/title, and organization.
5. Ask for exact confirmation with `I RATIFY` or `cancel`.
6. If not confirmed exactly, return the cancellation message.
7. Generate the ratification ID and ISO timestamp.
8. Create the ratification record from the charter snapshot plus identity data.
9. Display the success block and next steps.

## Practical Guidance

- If the charter has no explicit version, use `1.0`.
- If the charter has no formal agent name, derive one cleanly from the agent type or context.
- Preserve the exact authority boundary snapshot in the record.
- Keep the tone measured: this is an important act, but the user should still feel guided rather than intimidated.
