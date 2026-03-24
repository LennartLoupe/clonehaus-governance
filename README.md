# Clonehaus Governance Plugin

Deploy governed AI agents from clonehaus.ai into Cowork. Design governance on the platform, deploy in Cowork with full audit trail.

**Built for regulated industries facing the August 2026 EU AI Act deadline.**

---

## Prerequisites

- [Claude Cowork](https://claude.ai/cowork) (paid plan required)
- [clonehaus.ai account](https://clonehaus.ai) (sign up for free)
- At least one sealed agent on your clonehaus.ai account

---

## Installation

```bash
# Install the plugin
claude plugin add https://github.com/LennartLoupe/clonehaus-governance-v2

# Or install locally
git clone https://github.com/LennartLoupe/clonehaus-governance-v2.git
cd clonehaus-governance-v2
claude plugin install .
```

---

## Quick Start

### Step 1: Create Agent on Platform

1. Go to [clonehaus.ai](https://clonehaus.ai)
2. Create a new agent
3. Define authority boundaries (5 categories)
4. Ratify with named human
5. Agent status → SEALED

### Step 2: Generate API Key

1. Navigate to Settings → API Keys
2. Click "Generate New Key"
3. Copy the key (shown only once)

### Step 3: Connect Plugin

```text
/clonehaus:connect
```

Paste your API key when prompted.

### Step 4: Load Your Agent

```text
/clonehaus:list
/clonehaus:load "Your Agent Name"
```

Your governed agent is now active in Cowork! 🎉

---

## What This Plugin Does

**On the platform, you design and seal governance for every agent:**
- ✓ Decision authority (what they can and cannot decide)
- ✓ Data access boundaries (what data they can touch)
- ✓ External communication rules (who they can talk to)
- ✓ System access levels (what systems they can use)
- ✓ Escalation triggers (when they must ask for help)

**In Cowork, you deploy those governed agents into a live session:**
- ✓ Connect Cowork to your clonehaus.ai account
- ✓ Load sealed agents with named human accountability
- ✓ Run with embedded authority boundaries
- ✓ Send escalations back to the platform audit trail

---

## Commands

| Command | Description | Usage |
|---------|-------------|-------|
| `/clonehaus:connect` | Connect to your clonehaus.ai account | `/clonehaus:connect` |
| `/clonehaus:list` | Show your governed agents | `/clonehaus:list` |
| `/clonehaus:load` | Deploy an agent into Cowork | `/clonehaus:load "Agent Name"` |

---

## How It Works

**Design Time (clonehaus.ai platform):**
1. Create agent charter with 5 authority categories
2. Define what agent can/cannot do
3. Run workflow simulation
4. Ratify with named human
5. Agent sealed in database

**Runtime (Cowork plugin):**
1. Connect plugin to platform
2. Load sealed agent charter
3. Agent operates with embedded governance
4. Escalations logged back to platform
5. Full audit trail maintained

---

## Phase 2 Features

✅ **Platform Integration**
- Connect Cowork to your clonehaus.ai account
- Access all your sealed agents
- Real-time governance enforcement

✅ **Persistent Storage**
- Charters saved in database forever
- Access from any device
- Version history tracked

✅ **Real Audit Trail**
- All escalations logged to platform
- Named human accountability
- Compliance-ready documentation

✅ **Bidirectional Logging**
- Escalations flow back to platform
- Activity tracked in real-time
- Complete governance lifecycle

---

## Framework Support

Framework exports happen on the platform after your charter is designed and sealed, then the governed agent is deployed into Cowork.

### Supported Frameworks

- **LangChain** - Python runnable chain with GovernanceGuard
- **LangGraph** - StateGraph with authority checkpoint
- **CrewAI** - Agent with governance-mapped role/goal/backstory
- **N8N** - Importable JSON workflow with governance nodes
- **AutoGen** - ConversableAgent with reply_func guard
- **Semantic Kernel** - IFunctionInvocationFilter (Python & C#)

### Want to add a framework?

See [CONTRIBUTING.md](CONTRIBUTING.md) - we welcome PRs.

---

## Documentation

- [Installation Guide](docs/installation.md)
- [Quick Start Tutorial](docs/quickstart.md)
- [LangChain Integration](docs/frameworks/langchain.md)
- [N8N Integration](docs/frameworks/n8n.md)
- [EU AI Act Compliance](docs/compliance/eu-ai-act.md)

---

## Example: Platform-First Legal Agent

1. Create a Legal Advisory Agent on [clonehaus.ai](https://clonehaus.ai)
2. Set Decision Authority to Advisory (L2)
3. Limit Data Access to Confidential contract materials
4. Restrict External Communication to internal stakeholders
5. Add escalation triggers such as `liability > $500K` and non-standard terms
6. Ratify with your General Counsel and seal the agent
7. In Cowork, connect and load it:

```text
/clonehaus:connect
/clonehaus:list
/clonehaus:load "Legal Advisory Agent"
```

See [complete example](examples/legal_agent_example.md)

---

## Philosophy: Outside-the-Loop Governance

Clonehaus operates upstream of runtime behavior. Governance is designed at decision time on the platform, where humans can deliberate clearly, then deployed into Cowork with accountability intact.

We do not treat governance as an afterthought inside the session. The charter is created, reviewed, ratified, sealed, and then enforced when the agent runs.

**"We govern upstream so everything downstream runs cleaner."**

Read more: [clonehaus.ai/northstar](https://clonehaus.ai)

---

## EU AI Act Compliance

This plugin helps address:
- **Article 9** - Risk management system (authority boundaries + escalation)
- **Article 11** - Technical documentation (Agent Charter)
- **Article 13** - Transparency (CAN/CANNOT lists)
- **Article 14** - Human oversight (ratification records)

**Disclaimer:** This plugin is a tool to support compliance efforts, not a guarantee of compliance. Consult legal counsel for final validation.

---

## Development Status

**Current:** v0.2.0 (Phase 2 Platform Integration)
- ✓ Platform-connected Cowork workflow
- ✓ Sealed agent loading from clonehaus.ai
- ✓ Audit trail and escalation logging

**Next:**
- [ ] Expanded platform APIs
- [ ] Richer session telemetry
- [ ] Advanced compliance features

---

## Contributing

We welcome contributions. See [CONTRIBUTING.md](CONTRIBUTING.md)

**Ways to contribute:**
- Add new framework templates
- Improve documentation
- Report bugs
- Suggest features
- Share your use cases

---

## License

MIT License - see [LICENSE](LICENSE) for details

---

## Support

- **Platform:** [clonehaus.ai](https://clonehaus.ai)
- **GitHub:** [LennartLoupe/clonehaus-governance-v2](https://github.com/LennartLoupe/clonehaus-governance-v2)
- **Issues:** [GitHub Issues](https://github.com/LennartLoupe/clonehaus-governance-v2/issues)
- **Email:** info@clonehaus.ai

---

**Clonehaus Governance Plugin** | [Platform](https://clonehaus.ai) | [Documentation](docs/) | [Examples](examples/) | [GitHub](https://github.com/LennartLoupe/clonehaus-governance-v2)
