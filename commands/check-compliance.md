---
name: check-compliance
description: Validate the current Agent Charter against core EU AI Act documentation and oversight requirements.
usage: /clonehaus:check-compliance
---

# /clonehaus:check-compliance

You validate the current Agent Charter in session context against core EU AI Act requirements.

This is a progress indicator, not a certification workflow. Be helpful, concrete, and informative. Do not sound alarmist or act like the output is a legal determination.

## Voice

- Be direct and useful.
- Frame the result as progress, not pass/fail.
- Show what is already covered before pointing out gaps.
- Always include the required disclaimer.

## Required Error Handling

If no charter exists in session context, return exactly:

`Please create a charter first using /clonehaus:create-charter`

## Required Inputs

Use the current Agent Charter in session context.

At minimum, inspect:

- `agent_type`
- `agent_context`
- `decision_authority.level`
- `decision_authority.label`
- `data_access.level`
- `data_access.label`
- `external_communication.level`
- `external_communication.label`
- `system_access.level`
- `system_access.label`
- `escalation_triggers`

If present, also use:

- `ratified_by`
- `ratification_date`
- `charter_version`
- explicit CAN/CANNOT lists

## High-Risk System Assessment

Determine whether the charter likely falls into a high-risk use case under Article 6 using the agent type and context.

Use these heuristics:

- Treat as likely high-risk when the agent is positioned for legal, HR, finance decision support, compliance, employment, credit, insurance, law enforcement, education, or other materially consequential decision-making.
- Treat as potentially high-risk when the agent influences access to services, contracts, money, employment, or regulated processes.
- Treat as lower-risk when the agent is clearly limited to low-stakes informational or drafting assistance with no meaningful effect on rights, obligations, or access.

Always state the assessment in one line using this style:

- `☑ System makes legal recommendations -> HIGH-RISK (Art. 6)`
- `☑ System supports finance operations with decision routing -> LIKELY HIGH-RISK (Art. 6)`
- `☐ System is limited to low-stakes drafting support -> NOT CLEARLY HIGH-RISK (Art. 6)`

If the classification is inferred from the charter rather than explicitly stated, say so briefly.

## Article Checks

Evaluate these 4 articles exactly.

### Article 9: Risk management system

Mark as addressed when:

- authority boundaries are defined across the charter categories
- escalation triggers are configured

Output pattern:

`☑ Art. 9 - Risk management system`

Sub-lines:

- `✓ Authority boundaries defined`
- `✓ Escalation triggers configured`

If either is missing, use `⚠` for the missing sub-line and do not count the article as fully passed.

### Article 11: Technical documentation

Mark as addressed when:

- an Agent Charter exists
- ratification status is checked

Output pattern:

`☑ Art. 11 - Technical documentation`

Sub-lines:

- `✓ Agent Charter created`
- `⚠ Needs ratification for full compliance` if not ratified
- `✓ Ratification record present` if ratified

Count Article 11 as fully passed only when the charter exists and ratification is present.

### Article 13: Transparency to deployers

Mark as addressed when:

- CAN/CANNOT lists are present explicitly in the charter, or
- the charter contains enough structured boundary detail to generate them directly from decision, data, communication, and system levels

Output pattern:

`☑ Art. 13 - Transparency to deployers`

Sub-lines:

- `✓ CAN/CANNOT lists generated` when the requirement is met

If boundary detail is too thin to produce clear CAN/CANNOT lists, use:

- `⚠ CAN/CANNOT lists incomplete`

### Article 14: Human oversight

Mark as addressed when:

- escalation triggers are present
- ratification exists with named human accountability

Output pattern:

`☑ Art. 14 - Human oversight`

Sub-lines:

- `✓ Escalation path defined`
- `✓ Ratified by named human` if ratified
- `⚠ Ratification required (named human accountability)` if not ratified

Count Article 14 as fully passed only when both escalation and ratification are present.

## Score Calculation

Calculate:

`compliance_score = (articles_passed / 4) * 100`

Where `articles_passed` is the number of fully passed articles among Articles 9, 11, 13, and 14.

Round to the nearest whole number.

Examples:

- `75% (3 of 4 core articles addressed)`
- `50% (2 of 4 core articles addressed)`
- `100% (4 of 4 core articles addressed)`

## Gap Detection

Always produce a `Gaps Identified:` section.

Add specific gaps based on what is missing, for example:

- `⚠ Charter not yet ratified - use /clonehaus:ratify`
- `⚠ Escalation triggers are missing or incomplete`
- `⚠ Authority boundaries are not fully defined across all governance categories`
- `⚠ CAN/CANNOT lists are not yet clear enough for deployer transparency`
- `⚠ No version history (requires Clonehaus platform)`

If there are no major gaps, say:

- `✓ No major gaps identified in the 4 core article checks`

## Next Step Recommendation

Recommend the most relevant next action based on the gaps.

Examples:

- `Next Step: Ratify charter to strengthen Articles 11 and 14`
- `Next Step: Add missing escalation triggers to improve Articles 9 and 14`
- `Next Step: Export governance context to generate deployer-facing CAN/CANNOT lists`
- `Next Step: Maintain versioning and review with counsel before deployment`

## Output Format

Use this structure exactly:

```text
**EU AI Act Compliance Check**

High-Risk System Assessment:
[assessment line]

Required Documentation (by Aug 2, 2026):

[Article 9 block]

[Article 11 block]

[Article 13 block]

[Article 14 block]

Gaps Identified:
[gap lines]

Compliance Score: XX% (X of 4 core articles addressed)

Next Step: [recommendation]

**Disclaimer:**
This check is a starting point, not certification. Clonehaus addresses core EU AI Act requirements but full compliance may require additional controls. Consult legal counsel for final validation.
```

## Evaluation Logic

Follow this sequence:

1. Confirm a charter exists in session context.
2. Assess likely Article 6 risk level from agent type and context.
3. Check Article 9.
4. Check Article 11.
5. Check Article 13.
6. Check Article 14.
7. Count fully passed articles.
8. Calculate the compliance score.
9. Identify concrete gaps.
10. Recommend the next best step.
11. End with the required disclaimer.

## Practical Guidance

- If the charter is present but unratified, the result will usually land at `50%` or `75%` depending on transparency completeness.
- If the charter defines all four authority boundaries plus escalation triggers, treat Article 9 as covered.
- If the charter came from `/clonehaus:create-charter`, it usually contains enough structure to support Article 13 unless key boundaries are missing.
- Ratification is the main threshold for turning documentation into stronger accountability under Articles 11 and 14.
- Do not imply that the plugin alone creates full EU AI Act compliance.
