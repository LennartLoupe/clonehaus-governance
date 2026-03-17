# Changelog

All notable changes to the Clonehaus Governance Plugin will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned
- Agent-specific API keys (optional fine-grained access)
- Team collaboration features
- Advanced version control
- Real-time escalation notifications
- Usage analytics dashboard

## [0.2.0] - 2026-03-16

### 🎉 Major Release: Platform Integration

Phase 2 transforms the plugin from standalone charter creation to platform-connected agent deployment.

### Added

**Platform Connection:**
- `/clonehaus:connect` - Authenticate with clonehaus.ai account via API key
- `/clonehaus:list` - Show all sealed agents from platform
- `/clonehaus:load` - Deploy governed agent into Cowork session
- MCP protocol integration for platform API communication
- Secure API key storage and validation

**Features:**
- Persistent charter storage (agents saved in platform database)
- Real audit trail (escalations logged to platform in real-time)
- Bidirectional logging (agent activity flows back to platform)
- Platform-governed agent deployment (load sealed agents on demand)
- Multi-agent support (switch between different agents in same session)

**Documentation:**
- Phase 2 migration guide (`docs/phase2-migration.md`)
- Platform integration example (`examples/platform-integration-example.md`)
- Updated quick start guide for Phase 2 workflow
- Updated README with platform-first approach

### Changed

**Architecture:**
- Plugin role changed from charter creator to agent deployer
- Governance design now happens on clonehaus.ai platform (design time)
- Plugin focuses on runtime deployment (not design time)
- Updated governance skill to recommend platform-first workflow

**Commands:**
- Command structure simplified (3 commands vs 4 in Phase 1)
- All commands now interact with platform API
- Agent charters fetched from platform, not created locally

**Workflow:**
- Users must create agents on clonehaus.ai first
- API key required for plugin connection
- Agents loaded on-demand from platform
- Escalations automatically logged to platform

### Removed

**Phase 1 Standalone Commands:**
- `/clonehaus:create-charter` (now done on platform)
- `/clonehaus:export-context` (now done on platform)
- `/clonehaus:check-compliance` (now done on platform)
- `/clonehaus:ratify` (now done on platform)

**Templates:**
- Removed all 7 framework export templates (`templates/` directory)
- Framework exports now generated on platform, not in plugin

### Breaking Changes

⚠️ **Plugin now requires clonehaus.ai account**
- Users must sign up at https://clonehaus.ai
- API key required for plugin connection
- Phase 1 standalone mode no longer supported

⚠️ **Existing Phase 1 charters not migrated**
- Phase 1 charters were session-only (not saved)
- Users must recreate agents on platform
- See migration guide: `docs/phase2-migration.md`

### Migration

**For Phase 1 users:**
1. Create account at https://clonehaus.ai
2. Recreate agents on platform
3. Ratify agents (status → SEALED)
4. Generate API key (Settings → API Keys)
5. Connect plugin: `/clonehaus:connect`
6. Deploy agents: `/clonehaus:load`

See full migration guide: [docs/phase2-migration.md](docs/phase2-migration.md)

### Technical Details

**Platform API Integration:**
- 4 MCP endpoints: list-agents, get-agent, log-escalation, verify
- Bearer token authentication
- Real-time escalation logging
- Persistent storage in Supabase

**Security:**
- API keys hashed with bcrypt before storage
- Keys stored in plugin secure storage
- Key validation on every API call
- Automatic session expiry handling

### What's Next (Phase 2.5)

Planned for future releases:
- Agent-specific API keys (optional fine-grained access)
- Team collaboration features
- Advanced version control
- Real-time escalation notifications
- Usage analytics dashboard

---

## [0.1.0] - 2026-03-13

### Initial Release

**Features:**
- Standalone charter creation in Cowork
- Interactive `/create-charter` command
- Framework export templates (7 frameworks)
- EU AI Act compliance checking
- Ratification flow
- Governance skill

**Note:** Phase 1 has been superseded by Phase 2. See v0.2.0 for current workflow.
