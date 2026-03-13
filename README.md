# Clonehaus Governance Plugin

Define authority boundaries and create Agent Charters for your Claude Cowork agents. Export governance code for LangChain, N8N, CrewAI, and more.

**Built for regulated industries facing the August 2026 EU AI Act deadline.**

---

## 🚀 Quick Start
```bash
# Install the plugin
claude plugin add https://github.com/LennartLoupe/clonehaus-governance

# Or install locally
git clone https://github.com/LennartLoupe/clonehaus-governance.git
cd clonehaus-governance
claude plugin install .
```

In Cowork:
```
/clonehaus:create-charter
```

---

## 🎯 What This Plugin Does

**Before deploying AI agents, define:**
- ✓ Decision authority (what they can/cannot decide)
- ✓ Data access boundaries (what data they can touch)
- ✓ External communication rules (who they can talk to)
- ✓ System access levels (what systems they can use)
- ✓ Escalation triggers (when they must ask for help)

**Then export governance as working code for:**
- LangChain (Python)
- LangGraph (Python)
- CrewAI (Python)
- N8N (JSON workflow)
- AutoGen (Python)
- Semantic Kernel (Python & C#)

---

## 📖 Commands

| Command | Purpose |
|---------|---------|
| `/clonehaus:create-charter` | Interactive charter creation |
| `/clonehaus:export-context --framework=<n>` | Generate framework code |
| `/clonehaus:check-compliance` | Validate EU AI Act requirements |
| `/clonehaus:ratify` | Create accountability record |

---

## 🏗️ Framework Support

### Supported Now (v0.1.0)
- **LangChain** - Python runnable chain with GovernanceGuard
- **LangGraph** - StateGraph with authority checkpoint
- **CrewAI** - Agent with governance-mapped role/goal/backstory
- **N8N** - Importable JSON workflow with 5 nodes
- **AutoGen** - ConversableAgent with reply_func guard
- **Semantic Kernel** - IFunctionInvocationFilter (Python & C#)

### Want to add a framework?
See [CONTRIBUTING.md](CONTRIBUTING.md) - we welcome PRs!

---

## 📚 Documentation

- [Installation Guide](docs/installation.md)
- [Quick Start Tutorial](docs/quickstart.md)
- [LangChain Integration](docs/frameworks/langchain.md)
- [N8N Integration](docs/frameworks/n8n.md)
- [EU AI Act Compliance](docs/compliance/eu-ai-act.md)

---

## 🎓 Example: Legal Agent
```
/clonehaus:create-charter

Agent Type: Legal
Decision Authority: Advisory (can recommend, cannot approve)
Data Access: Confidential (NDAs, contracts - no privileged comms)
External Comms: Internal only
System Access: Read-only
Escalation: >$500K liability, non-standard terms

/clonehaus:export-context --framework=langchain

✓ Generated: clonehaus_legal_agent.py
```

See [complete example](examples/legal_agent_example.md)

---

## 🔒 Philosophy: Outside-the-Loop Governance

Clonehaus operates **upstream of deployment** - at design time, where humans can deliberate.

We don't monitor your agents at runtime. We help you define what they're allowed to do before they run.

**"We govern upstream so everything downstream runs cleaner."**

Read more: [clonehaus.ai/northstar](https://clonehaus.ai)

---

## 🏛️ EU AI Act Compliance

This plugin helps address:
- **Article 9** - Risk management system (authority boundaries + escalation)
- **Article 11** - Technical documentation (Agent Charter)
- **Article 13** - Transparency (CAN/CANNOT lists)
- **Article 14** - Human oversight (ratification records)

**Disclaimer:** This plugin is a tool to support compliance efforts, not a guarantee of compliance. Consult legal counsel for final validation.

---

## 🛠️ Development Status

**Current:** v0.1.0 (Standalone Plugin)
- ✓ Local charter creation
- ✓ Framework code generation
- ✓ Basic compliance checking

**Next:** v0.2.0 (Platform Integration)
- [ ] MCP integration
- [ ] Persistent storage
- [ ] Version history
- [ ] Advanced compliance features

---

## 🤝 Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md)

**Ways to contribute:**
- Add new framework templates
- Improve documentation
- Report bugs
- Suggest features
- Share your use cases

---

## 📄 License

MIT License - see [LICENSE](LICENSE) for details

---

## 💬 Support

- **Issues:** [GitHub Issues](https://github.com/LennartLoupe/clonehaus-governance/issues)
- **Discussions:** [GitHub Discussions](https://github.com/LennartLoupe/clonehaus-governance/discussions)
- **Email:** info@clonehaus.ai
- **Website:** [clonehaus.ai](https://clonehaus.ai)

---

## 🌟 Acknowledgments

Built for the AI governance community.

Special thanks to:
- Anthropic for Claude Cowork
- The LangChain, CrewAI, and N8N communities
- Early testers and contributors

---

**Clonehaus Governance Plugin** | [Documentation](docs/) | [Examples](examples/) | [Changelog](CHANGELOG.md)