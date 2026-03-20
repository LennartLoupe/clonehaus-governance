# Integrating Clonehaus Governance with LangChain

LangChain is a strong fit when you want governed prompts, reusable chains, and clear application-level control around model calls. Governance matters here because the fastest path to shipping an agent is often a direct prompt-and-run loop, which is also the easiest place to blur authority boundaries if you do not define them up front.

## Prerequisites

- Clonehaus Governance Plugin installed
- Python 3.10+
- LangChain and `langchain-anthropic` installed
- Agent Charter created with `/clonehaus:create-charter`

Example install:

```bash
pip install langchain langchain-anthropic anthropic
```

## Export Your Governance Code

```text
/clonehaus:export-context --framework=langchain
```

## What Gets Generated

The export generates a Python file like:

- `clonehaus_legal_review_langchain.py`

The file includes:

- A `GOVERNANCE_BLOCK` that embeds the charter into the system prompt
- A `GovernanceGuard` that checks decision, data, communication, and system boundaries
- Escalation handling through `AuthorityViolation` and `EscalationRequired`
- A `create_governed_agent()` helper that wires `ChatAnthropic`, `PromptTemplate`, and `LLMChain`

Approximate size:

- 200-300 lines depending on the charter content

## Integration Steps

### Step 1: Export and place the generated file in your app

Run the export command and save the generated file somewhere importable by your application, for example:

```text
app/
  agents/
    clonehaus_legal_review_langchain.py
```

### Step 2: Create the governed runnable

The generated file already wires the governance block into the prompt and wraps the model call with the guard.

```python
from app.agents.clonehaus_legal_review_langchain import create_governed_agent

agent = create_governed_agent(
    anthropic_api_key="YOUR_ANTHROPIC_API_KEY",
)
```

If you want to pass an explicit authority context override at runtime, you can:

```python
from app.agents.clonehaus_legal_review_langchain import (
    GOVERNANCE_BLOCK,
    create_governed_agent,
)

agent = create_governed_agent(
    authority_context={
        "agent_name": "Legal Review Agent",
        "decision_level": "ADVISORY",
        "decision_label": "Advisory",
        "data_ceiling": "CONFIDENTIAL",
        "data_label": "Confidential",
        "comm_scope": "INTERNAL_ONLY",
        "comm_label": "Internal Only",
        "system_access": "READ_ONLY",
        "system_label": "Read-Only",
        "escalation_triggers": "- scope boundary\n- ambiguity\n- liability > $500K",
        "governance_block": GOVERNANCE_BLOCK,
    },
    anthropic_api_key="YOUR_ANTHROPIC_API_KEY",
)
```

### Step 3: Pass action metadata before every run

The governance checks are strongest when you describe the intended action explicitly.

```python
result = agent(
    "Review this NDA and summarize the indemnity and liability risks.",
    action={
        "decision_level": "ADVISORY",
        "data_classification": "CONFIDENTIAL",
        "recipient_scope": "INTERNAL_ONLY",
        "system_access": "READ_ONLY",
        "risk_flags": [],
    },
    context={"matter_id": "nda-2048"},
)

print(result)
```

### Step 4: Test the governed agent

Start with one request that should pass and one that should fail.

Allowed example:

```python
agent(
    "Summarize the major legal risks in this supplier agreement.",
    action={
        "decision_level": "ADVISORY",
        "data_classification": "CONFIDENTIAL",
        "recipient_scope": "INTERNAL_ONLY",
        "system_access": "READ_ONLY",
    },
)
```

Violation example:

```python
agent(
    "Approve this contract and email it back to the vendor.",
    action={
        "decision_level": "TRANSACTIONAL",
        "data_classification": "CONFIDENTIAL",
        "recipient_scope": "PARTNER",
        "system_access": "WRITE_LIMITED",
    },
)
```

## Key Features

**Authority Enforcement:**
The generated `GovernanceGuard` checks requested decision level, data classification, recipient scope, and system access against the charter before the model runs. This keeps authority logic outside prompt wording alone.

**Escalation Handling:**
When a request hits a configured trigger or exceeds scope, the generated code raises `EscalationRequired` or `AuthorityViolation`. Your application can catch that and route the request to human review.

**Customization:**
You can modify prompt wording, model temperature, and runtime context plumbing. Do not loosen the authority rank maps or remove escalation checks unless you intend to change the underlying charter.

## Example Usage

```python
from clonehaus_legal_review_langchain import (
    AuthorityViolation,
    EscalationRequired,
    create_governed_agent,
)


def main() -> None:
    agent = create_governed_agent(anthropic_api_key="YOUR_ANTHROPIC_API_KEY")

    try:
        result = agent(
            "Review this NDA and summarize the main commercial risks.",
            action={
                "decision_level": "ADVISORY",
                "data_classification": "CONFIDENTIAL",
                "recipient_scope": "INTERNAL_ONLY",
                "system_access": "READ_ONLY",
                "risk_flags": [],
            },
            context={"request_id": "demo-001"},
        )
        print(result)
    except AuthorityViolation as exc:
        print(f"Blocked by governance: {exc}")
    except EscalationRequired as exc:
        print(f"Escalation required: {exc.reason}")


if __name__ == "__main__":
    main()
```

## Troubleshooting

**Common Issue 1: `ModuleNotFoundError: langchain_anthropic`**
Install the provider package explicitly with `pip install langchain-anthropic`.

**Common Issue 2: Requests fail without authority checks doing anything**
Make sure you pass `action={...}` metadata into the governed callable. The prompt still contains the governance block, but the hard checks only work when the code can compare the requested action to the charter.

**Common Issue 3: Prompt performance feels repetitive**
Use LangChain prompt caching or application-side response caching when your governance block is stable across requests. This works especially well because the authority context changes much less often than the user message.

## Next Steps

- Review the generated code comments for the exact guard behavior
- See the full walkthrough in [legal_agent_example.md](/Users/lennartzanders/dev_clean/clonehaus-governance/examples/legal_agent_example.md)
- Export the same charter to another framework if you need a different runtime shape
