# EU AI Act Compliance Guide

## Overview

The EU AI Act (Regulation (EU) 2024/1689) requires specific governance, documentation, and oversight controls for certain AI systems, especially high-risk systems.

**Key date:** `2 August 2026` is the Act's general application date for most provisions.  
Important nuance: as of March 13, 2026, the European Commission has also said some high-risk timing may shift because the Digital Omnibus proposal would link parts of the high-risk regime to the availability of support tools such as standards. Treat `2 August 2026` as the main planning date, but monitor official updates closely.

This guide explains:

- Whether your AI agent is high-risk
- What the Act requires
- How Clonehaus addresses those requirements
- What else you need for full compliance

---

## Is Your Agent High-Risk?

Under Article 6 and Annex III, AI systems are high-risk if they are:

- safety components of certain regulated products, or
- intended for specific high-risk use cases listed in Annex III

The classification depends on the system's **intended purpose**, not just the industry label attached to it.

**Employment & HR (Annex III, Section 4):**

- Recruitment, screening, or evaluation of candidates
- Task allocation or performance monitoring
- Promotion or termination decisions

**Critical Infrastructure (Annex III, Section 2):**

- Safety components used in digital infrastructure, road traffic, or the supply of water, gas, heating, or electricity

**Education and vocational training:**

- Evaluating learning outcomes
- Steering the learning process
- Monitoring cheating in relevant contexts

**Essential private and public services:**

- Creditworthiness assessment of natural persons
- Risk and pricing decisions for life and health insurance
- Certain access decisions affecting essential services or benefits

**Law enforcement, migration, border control, justice, and democratic processes:**

- Certain law-enforcement use cases
- Certain migration or border-control use cases
- Certain administration-of-justice and democratic-process use cases

**Biometrics:**

- Certain remote biometric identification, biometric categorisation, and emotion-recognition use cases, where permitted and not prohibited elsewhere in the Act

**Example classifications:**

- ✓ HR agent screening candidates -> HIGH-RISK
- ✓ Credit or insurance decision-support agent -> HIGH-RISK
- ✓ AI used in administration-of-justice use cases -> HIGH-RISK
- ⚠ Legal advisory agent reviewing contracts -> MAY BE HIGH-RISK depending on intended purpose and deployment context
- ✗ Sales CRM assistant -> usually NOT HIGH-RISK unless it moves into an Annex III use case
- ✗ Internal chatbot answering FAQs -> usually NOT HIGH-RISK

**Important note on legal agents:**  
Not every legal-support tool is automatically Annex III high-risk. A contract-review assistant for an in-house legal team is not necessarily the same thing as an AI system used in administration of justice. If the use case is legally consequential or close to regulated decision-making, get legal advice instead of relying on a shortcut classification.

If unsure, consult legal counsel.

---

## Key Requirements for High-Risk Systems

### Article 9: Risk Management System

**Requirement:**  
Establish an iterative risk management system across the AI system lifecycle.

**Clonehaus Coverage:**

- ✓ Authority boundaries define risk parameters before deployment
- ✓ Escalation triggers create risk-based human intervention points
- ✓ Charter structure makes risk assumptions explicit and reviewable

**What else you need:**

- Ongoing risk assessment process
- Testing and validation procedures
- Post-deployment monitoring
- Corrective-action process when risks change in practice

---

### Article 11: Technical Documentation

**Requirement:**  
Maintain technical documentation that demonstrates how the system is designed, governed, and used.

**Clonehaus Coverage:**

- ✓ Agent Charter = structured governance specification
- ✓ Authority Context / exported governance code = implementation-facing documentation
- ✓ Ratification record = accountability documentation tied to a named human
- ✓ Framework exports = evidence of how governance is embedded into the stack

**What to retain:**

- Agent Charter
- Ratification record with named human
- All charter versions
- Exported framework code
- Internal notes showing how the deployed system matches the charter

**What else you need:**

- Broader technical documentation expected for the actual deployed system
- Records showing how the system was tested, validated, and updated

---

### Article 13: Transparency to Deployers

**Requirement:**  
Deployers need to understand the system's capabilities, limitations, and oversight conditions.

**Clonehaus Coverage:**

- ✓ CAN/CANNOT boundary logic across authority categories
- ✓ Clear authority level labels
- ✓ Escalation triggers documented in plain language
- ✓ Governance exports that make boundaries visible to technical implementers

**Example transparency output:**

This agent CAN:

- Analyze contracts and flag risks
- Recommend approval or changes

This agent CANNOT:

- Approve contracts
- Access privileged communications
- Make binding commitments

This agent WILL ESCALATE when:

- Liability exceeds $500K
- The request is ambiguous or outside scope

**What else you need:**

- Internal deployer instructions
- User-facing or operator-facing documentation where relevant
- Training so staff understand what the system is and is not allowed to do

---

### Article 14: Human Oversight

**Requirement:**  
Design and use the system so effective human oversight is possible in practice.

**Clonehaus Coverage:**

- ✓ Ratification creates named human accountability at design time
- ✓ Escalation triggers define when the agent must stop and hand off
- ✓ Authority ceilings limit what the system can do autonomously

**Phase 1 (Plugin):**

- Ratification creates an oversight and accountability record
- Escalation triggers define when human intervention is required

**Phase 2 (Platform):**

- Planned stronger audit trail and persistence features
- Planned version history and richer governance operations

**What else you need:**

- Real operational oversight procedures
- Staff who are actually empowered to intervene
- Monitoring and incident handling after deployment

---

## Compliance Checklist

Use this to track your compliance effort:

- [ ] Determine whether your agent is high-risk under Article 6 and Annex III
- [ ] Create Agent Charter with `/clonehaus:create-charter`
- [ ] Define all 5 authority categories
- [ ] Configure escalation triggers
- [ ] Ratify charter with named human via `/clonehaus:ratify`
- [ ] Retain the charter and ratification record
- [ ] Validate with `/clonehaus:check-compliance`
- [ ] Export and retain integration code via `/clonehaus:export-context`
- [ ] Establish ongoing monitoring and incident handling outside Clonehaus
- [ ] Consult legal counsel for final validation

---

## What Clonehaus Does NOT Cover

Be explicit about the gaps.

**Clonehaus addresses:**

- ✓ Pre-deployment governance design
- ✓ Authority boundary specification
- ✓ Escalation planning
- ✓ Named human accountability through ratification
- ✓ A documentation foundation for Articles 9, 11, 13, and 14

**Clonehaus does NOT fully address:**

- ✗ Article 10 data and data-governance obligations
- ✗ Article 12 logging and traceability infrastructure
- ✗ Article 15 accuracy, robustness, and cybersecurity controls
- ✗ Article 17 quality management system for providers of high-risk AI systems
- ✗ Article 27 fundamental rights impact assessment where required
- ✗ Conformity assessment obligations
- ✗ Registration and broader provider/deployer obligations where applicable
- ✗ Post-market monitoring and incident reporting operations

**For fuller compliance, you may also need:**

- Data governance controls
- Logging and traceability systems
- Validation, testing, and quality management processes
- Fundamental-rights impact assessment in relevant cases
- Legal review of provider vs deployer obligations
- Ongoing monitoring infrastructure

---

## Compliance Score Explained

When you run `/clonehaus:check-compliance`, the score reflects how completely the plugin-side governance pieces are in place.

**75-100%: Strong foundation**

- Charter is in place
- Governance boundaries are clear
- Ratification may be complete
- Core plugin-side checks are largely covered

**50-74%: Good progress**

- Charter exists
- Major governance elements are present
- Ratification or other key documentation pieces are still missing

**Below 50%: Incomplete**

- Charter is missing or incomplete
- Governance boundaries are not fully defined
- Important gaps remain before review or deployment

**Important note:**  
Even a `100%` score means the Clonehaus plugin-side governance components are complete. It does **not** mean your system is fully compliant with the EU AI Act.

---

## Important Disclaimers

⚠️ **This plugin is a foundation, not a certification tool:**

- Clonehaus helps with core governance and documentation work
- Full compliance requires additional technical, operational, and legal controls
- You should involve qualified legal counsel before relying on any compliance conclusion

⚠️ **The timing is still evolving:**

- `2 August 2026` remains the main general application date in official Commission materials
- The Commission has also proposed adjustments to some high-risk timing because standards are delayed
- Monitor official EU updates instead of assuming the timeline is frozen

⚠️ **High-risk classification is context-specific:**

- Classification depends on intended purpose and deployment context
- Not every system in a legal, HR, or finance environment is automatically Annex III high-risk
- Borderline cases should be reviewed by counsel

⚠️ **You remain responsible:**

- Clonehaus provides tools and documentation patterns
- It does not replace your compliance function, your risk team, or your legal advisors

---

## Additional Resources

**Official EU resources:**

- EU AI Act overview: https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai
- AI Act FAQ and implementation guidance: https://digital-strategy.ec.europa.eu/en/faqs/navigating-ai-act
- AI Act standardisation and timing context: https://digital-strategy.ec.europa.eu/en/policies/ai-act-standardisation
- Regulation (EU) 2024/1689 on EUR-Lex: https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32024R1689

**Clonehaus resources:**

- Check compliance: `/clonehaus:check-compliance`
- Create charter: `/clonehaus:create-charter`
- Legal example: [legal_agent_example.md](/Users/lennartzanders/dev_clean/clonehaus-governance/examples/legal_agent_example.md)
- Support: `info@clonehaus.ai`

**Next steps:**

1. Create your charter with `/clonehaus:create-charter`
2. Validate the governance foundation with `/clonehaus:check-compliance`
3. Ratify the charter with `/clonehaus:ratify`
4. Review the result with legal counsel before deployment

---

Built for regulated industries. Not a substitute for legal advice.
