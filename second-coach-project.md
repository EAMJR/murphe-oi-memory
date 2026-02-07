# Second Coach Project - Complete Reference

## The Business
AI-powered performance intelligence for professional athletes.

**Repository:** https://github.com/EAMJR/second-coach

## Model (Flipped)

| Phase | Service | Monthly Price | Length | What You Do |
|-------|---------|---------------|--------|-------------|
| **Phase 1** | Performance Intelligence | $5,000-7,000 | 5-7 hrs/week | Game scouting, film analysis, patterns, recovery correlation |
| **Phase 2** | + Off-Court Concierge | +$3,000-4,000 | +2-4 hrs/week | Email, finance, travel, brand (optional add-on) |

**Why Performance First:**
1. Measurable ROI ("Your mid-range improved 8%")
2. Lower barrier (no sensitive data Day 1)
3. Higher perceived value
4. Trust before access

## Architecture

```
HUB (Python FastAPI + Postgres + Redis)
├─ REST API: /opponent/TEAM, /player/ID/trends
├─ Ingests game data (Synergy API)
├─ Cache: 6-24 hour TTL
└─ Serves to all clients

CLIENTS (OpenClaw, one per athlete)
├─ Container per client (isolation)
├─ Telegram interface
├─ Sub-agent spawning for parallel analysis
├─ Cache from Hub
└─ Delivers personalized reports
```

## Repository Structure

| Component | Files | Purpose |
|-----------|-------|---------|
| **Hub** | main.py, docker-compose.yml, Dockerfile, requirements.txt, init.sql, seed_mock_data.py | FastAPI service with 5 endpoints |
| **Scripts** | mvp-bootstrap.sh, new-client.sh, deploy-skills.sh, hub-health.sh | Operations automation |
| **Client Template** | docker-compose.yml, SOUL.md.template, USER.md.template | Base for new athletes |
| **Skills** | test-hub-query/skill.py | Hub connectivity test |
| **Docs** | architecture.md, operations.md, phase1-skills.md, phase2-skills.md, sub-agents.md, onboarding.md | 8 comprehensive guides |

## Key API Endpoints

- `GET /health` - Hub status
- `GET /opponent/{team}` - Defensive tendencies, key defenders
- `GET /player/{id}/trends` - Rolling stats, zone efficiency
- `GET /matchup/{p}/vs/{o}` - Historical head-to-head
- `GET /recovery/{id}/correlation` - Sleep vs performance

## Execution Plan

**Phase 1: Infrastructure (15 min)**
```bash
cd hub && docker-compose up -d
curl localhost:8080/health
```

**Phase 2: Database (5 min)**
```bash
psql -f init.sql
python seed_mock_data.py
```

**Phase 3: Mock Client (10 min)**
```bash
./scripts/new-client.sh "mock-001" "Test Athlete"
# Configure Telegram bot token
# docker-compose up -d
```

**Phase 4: Test (10 min)**
```bash
./scripts/hub-health.sh
```

**Or one command:**
```bash
./scripts/mvp-bootstrap.sh
```

## Scaling

| Clients | Revenue | Hours/Week | Setup |
|---------|---------|------------|--------|
| 5 | $25-35k | 25-30 | Single VPS |
| 8 | $40-56k | 40-45 | Target zone |
| 10 | $50-70k | 50-55 | Dedicated client host |
| 12 | $60-84k | 65+ | **Hire** |

## The Value Prop

For athlete:
- "I'll spot the 2-3 adjustments per week that keep you in the league 2 years longer"
- Teams have analytics, but serve COACHES, not individual development
- You bridge that gap

For you:
- $50-70k/month solo (manageable with sub-agents)
- Market: Established pros ($5M+ net worth)
- Entry: Former athletes, year 3-5 players, post-injury

## What's Working (Post-Execute)

- [ ] Hub running on :8080
- [ ] Postgres tables created
- [ ] Mock data seeded (5 players, 10 games)
- [ ] Client container spawned
- [ ] Telegram bot responding
- [ ] Sub-agents completing in <5 min
- [ ] Pre-game report generates

## Next When Ready

1. **Replace mock data** → Real Synergy API (need $500/mo subscription)
2. **Add Client #2** → Duplicate, test multi-client
3. **First real athlete** → Unpaid trial, prove value

## Key Decisions Made

1. **Performance first** (not concierge) - Better entry point
2. **Hub + Client architecture** - Python for compute, OpenClaw for personalization
3. **Sub-agents critical** - Parallel analysis = solo scalability
4. **Private repo** - Business plans, pricing, ops
5. **Phase-based approach** - Build incrementally, validate each step

## Costs

| Item | Monthly |
|------|---------|
| VPS (Hub + DB) | $60-100 |
| Synergy API | $500 |
| Second Spectrum (opt) | $1,000 |
| **Total** | **$560-1,600** |

Revenue at 10 clients: $50-70k/month. Margin: 97%.

## Links

- Repo: https://github.com/EAMJR/second-coach
- Detailed README: /README-detailed.md
- Execution Plan: /EXECUTION-PLAN.md
- Docs: /docs/

## Status: READY TO EXECUTE

Execute when:
- VPS with Docker available
- Optionally: Synergy API key
- Decision: First test client (friend or actual athlete)

Command: `./scripts/mvp-bootstrap.sh`