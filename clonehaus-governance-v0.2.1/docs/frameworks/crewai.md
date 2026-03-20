# Integrating Clonehaus Governance with CrewAI

CrewAI is useful when you want agents to collaborate on tasks while still keeping their roles explicit. Governance matters here because multi-agent setups can blur responsibility quickly unless authority, delegation, tool access, and escalation behavior are pinned to a clear charter.

## Prerequisites

- Clonehaus Governance Plugin installed
- Python 3.10+
- CrewAI installed
- Agent Charter created with `/clonehaus:create-charter`

Example install:

```bash
pip install crewai
```

## Export Your Governance Code

```text
/clonehaus:export-context --framework=crewai
```

## What Gets Generated

The export generates a Python file like:

- `clonehaus_finance_ops_crewai.py`

The file includes:

- A `GOVERNANCE_BLOCK` with the full authority boundary set
- A governed `Agent` factory that maps the charter into role, goal, and backstory
- Tool restriction logic based on decision authority
- Delegation rules based on authority level

Approximate size:

- 80-150 lines depending on the charter and generated comments

## Integration Steps

### Step 1: Export and place the generated file in your CrewAI project

Save the exported file somewhere importable by your app, for example:

```text
app/
  crews/
    clonehaus_finance_ops_crewai.py
```

### Step 2: Attach only the tools the charter should allow

The generated file already narrows the tool list based on decision authority:

- L1: no tools
- L2: first tool only
- L3: first two tools
- L4-L5: broader tool access

That means tool order matters. Put the safest and most important tools first.

```python
from app.crews.clonehaus_finance_ops_crewai import create_governed_agent


def read_invoice(invoice_id: str) -> str:
    return f"Invoice details for {invoice_id}"


def update_invoice_status(invoice_id: str, status: str) -> str:
    return f"Updated {invoice_id} to {status}"


agent = create_governed_agent(
    tools=[read_invoice, update_invoice_status],
)
```

### Step 3: Create tasks that stay inside the charter

CrewAI works best when tasks are narrowly scoped to the chartered authority.

```python
from crewai import Crew, Task
from app.crews.clonehaus_finance_ops_crewai import create_governed_agent


def read_invoice(invoice_id: str) -> str:
    return f"Invoice details for {invoice_id}"


def update_invoice_status(invoice_id: str, status: str) -> str:
    return f"Updated {invoice_id} to {status}"


agent = create_governed_agent(tools=[read_invoice, update_invoice_status])

task = Task(
    description="Review invoice INV-2048, categorize it, and route it to the right approver.",
    expected_output="A routing recommendation and status update that stays inside charter limits.",
    agent=agent,
)

crew = Crew(agents=[agent], tasks=[task], verbose=True)
```

### Step 4: Test the governed agent

Run one routine task and one task that should stay human-controlled.

Allowed example:

```python
Task(
    description="Categorize this invoice and route it to procurement approval.",
    expected_output="Suggested route and updated invoice status.",
    agent=agent,
)
```

Not appropriate for an L2-L3 governed finance agent:

```python
Task(
    description="Approve this payment and update the vendor's banking details.",
    expected_output="Payment approval completed.",
    agent=agent,
)
```

## Key Features

**Authority Enforcement:**
CrewAI itself does not provide the governance model. The generated file maps the charter into role, goal, backstory, tool availability, and delegation permissions so the agent is shaped by authority from the start.

**Escalation Handling:**
Escalation is expressed through the charter-backed backstory and by keeping unsafe tools and delegation paths out of reach. In higher-control environments, you should combine this with application-side checks before executing sensitive tasks.

**Customization:**
You can refine the agent role wording, expected outputs, and tool implementations. You should not silently add tools or enable delegation beyond what the charter supports, because that changes the effective authority of the agent.

## Example Usage

```python
from crewai import Agent, Crew, Task
from clonehaus_finance_ops_crewai import create_governed_agent


def read_invoice(invoice_id: str) -> str:
    return f"Invoice details for {invoice_id}"


def update_invoice_status(invoice_id: str, status: str) -> str:
    return f"Updated {invoice_id} to {status}"


def main() -> None:
    finance_agent = create_governed_agent(
        tools=[read_invoice, update_invoice_status],
    )

    task = Task(
        description="Review invoice INV-2048, categorize it, and route it to the correct approver.",
        expected_output="A concise routing recommendation and any required status update.",
        agent=finance_agent,
    )

    crew = Crew(agents=[finance_agent], tasks=[task], verbose=True)
    print(crew.kickoff())


if __name__ == "__main__":
    main()
```

## Multi-Agent Considerations

- Give each agent its own charter if their authority differs
- Do not assume a reviewer agent can inherit the same authority as an execution agent
- Keep delegation disabled for L1-L2 agents
- For L3+ agents, allow delegation only when the downstream agent is governed at an equal or narrower scope

## Troubleshooting

**Common Issue 1: The wrong tools are available**
Check the order of the tools you pass into `create_governed_agent()`. Lower-authority agents only receive the first one or two tools.

**Common Issue 2: Delegation is unexpectedly disabled**
That is usually because the exported charter maps to L1 or L2. In the generated file, delegation only opens at L3 and above.

**Common Issue 3: The agent still sounds too broad**
Tighten the task description and expected output. CrewAI behavior improves when task scope matches the charter rather than assuming the backstory alone will do all the work.

## Next Steps

- Review the generated code comments before adding real production tools
- See the full walkthrough in [finance_agent_example.md](/Users/lennartzanders/dev_clean/clonehaus-governance/examples/finance_agent_example.md)
- Add stronger runtime controls around any tool that can change real systems or financial state
