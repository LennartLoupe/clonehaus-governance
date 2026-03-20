# Migrating to Phase 2: Platform Integration

## What Changed in Phase 2

### Phase 1 (Standalone Plugin)
- Created charters directly in Cowork
- Charters existed only in your session
- No persistent storage
- Ratification records not saved
- Limited to single device/session

### Phase 2 (Platform Connected)
- Design governance on clonehaus.ai platform
- Persistent storage in database
- Real audit trail with escalation logging
- Access agents from any device
- Ratification records permanently saved
- Full organizational control

---

## Breaking Changes

### Commands Removed
The following commands no longer exist in the plugin:

- `/clonehaus:create-charter` → Now done on clonehaus.ai
- `/clonehaus:export-context` → Now "Export" button on platform
- `/clonehaus:check-compliance` → Now compliance checker on platform
- `/clonehaus:ratify` → Now ratification flow on platform

### New Commands
- `/clonehaus:connect` → Authenticate with your platform account
- `/clonehaus:list` → Show your sealed agents from platform
- `/clonehaus:load` → Deploy a governed agent into Cowork

---

## Migration Steps

### Step 1: Create Platform Account

If you don't have a clonehaus.ai account:

1. Go to https://clonehaus.ai
2. Sign up (free account available)
3. Create your organization
4. You're now ready to create agents

### Step 2: Recreate Your Agents on Platform

For each agent you created in Phase 1:

1. **Navigate to clonehaus.ai**
2. **Create new agent:**
   - Click "Register New Agent"
   - Fill in: Name, Type, Context
3. **Define authority boundaries:**
   - Decision Authority (L1-L5)
   - Data Access (L1-L4)
   - External Communication (L1-L6)
   - System Access (L1-L4)
   - Escalation Triggers
4. **Review auto-generated LPS**
5. **Ratify the charter:**
   - Enter your name and role
   - Type "I RATIFY"
   - Charter status → SEALED
6. **Repeat for all agents**

**Note:** If you saved your Phase 1 charters, use them as reference for the authority levels.

### Step 3: Generate API Key

**Important:** Only organization administrators should generate API keys.

1. Go to Settings → API Keys
2. Click "Generate New Key"
3. Copy the key (shown only once!)
4. Store securely (password manager recommended)
5. Share with authorized users only

### Step 4: Update Plugin to v0.2.0

The plugin should auto-update, but verify:

1. Check plugin version in Cowork
2. Should show: clonehaus-governance v0.2.0
3. If not updated, reinstall:

```bash
claude plugin remove clonehaus-governance
claude plugin add https://github.com/LennartLoupe/clonehaus-governance
```

### Step 5: Connect Plugin to Platform

In Cowork:

1. Run `/clonehaus:connect`
2. Paste your API key when prompted
3. Verify connection shows your email and organization
4. You're connected! ✓

### Step 6: Deploy Your Agents

1. Run `/clonehaus:list` to see your sealed agents
2. Run `/clonehaus:load "Agent Name"` to deploy
3. Agent now operates with platform-defined governance
4. All escalations logged to platform audit trail

---

## What You Gain in Phase 2

### Persistent Storage
✅ Charters saved in database forever
✅ Access from any device
✅ Never lose your governance configuration

### Real Audit Trail
✅ All escalations logged to platform
✅ Complete governance lifecycle tracked
✅ Compliance-ready documentation

### Platform Features
✅ Workflow simulation (check for agent conflicts)
✅ Framework exports (LangChain, N8N, etc.)
✅ Organization hierarchy (coming in Phase 2.5)
✅ Team collaboration (coming in Phase 2.5)

### Better Governance
✅ Centralized control (admins create, users consume)
✅ Named accountability (ratification records saved)
✅ EU AI Act compliance tracking
✅ Version history

---

## Recommended Workflow (Best Practices)

### For Organization Administrators:

1. **Design governance on platform** (design time)
   - Define all agents centrally
   - Run simulations to check conflicts
   - Ratify with appropriate authority
   - Seal agents for deployment

2. **Generate one API key**
   - Share with authorized users only
   - Rotate regularly for security
   - Revoke if compromised

3. **Monitor activity**
   - Check escalation logs on platform
   - Review agent performance
   - Update governance as needed

### For End Users:

1. **Request API key** from your admin
2. **Connect once** (`/clonehaus:connect`)
3. **Load agents as needed** (`/clonehaus:load`)
4. **Work within boundaries** (escalations logged)

---

## Troubleshooting

### "Cannot find any agents"
→ Make sure agents are SEALED on platform (not DRAFT)
→ Check you're connected to correct organization

### "Invalid API key"
→ Key may have been revoked
→ Generate new key on platform
→ Reconnect with `/clonehaus:connect`

### "Agent not found"
→ Use `/clonehaus:list` to see exact agent names
→ Matching is case-insensitive, but using the exact agent name helps avoid ambiguity

### "Session expired"
→ Run `/clonehaus:connect` again
→ API keys don't expire unless revoked

---

## FAQ

**Q: Can I still use Phase 1 plugin?**
A: No, Phase 1 commands have been removed. Phase 2 is the new standard.

**Q: Do I need to pay for clonehaus.ai?**
A: Free accounts are available. Paid plans offer additional features.

**Q: Can I keep my old charters?**
A: Phase 1 charters weren't saved unless you exported them. You'll need to recreate them on the platform.

**Q: Who should generate API keys?**
A: Only organization administrators/governance leads should generate and distribute API keys.

**Q: Can I use multiple agents in one session?**
A: Yes! Load different agents as needed with `/clonehaus:load`. Each maintains its own governance.

**Q: Where are escalations logged?**
A: All escalations are logged to your clonehaus.ai audit trail in real-time.

---

## Need Help?

- **Documentation:** https://github.com/LennartLoupe/clonehaus-governance/tree/main/docs
- **Support:** info@clonehaus.ai
- **Platform:** https://clonehaus.ai

---

**Ready to migrate? Start with Step 1: Create your platform account at clonehaus.ai**
