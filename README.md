# Capstone Radar

> Unified A-F grading and ship/no-ship decisions for the 5-skill radar family.

## What It Does

Capstone Radar is the aggregator and gap filler for the radar family. It combines results from 4 companion audit skills with its own security, testing, and code quality scans, then grades your entire codebase on one unified scale and tells you whether it's safe to ship.

It owns 5 domains that the companion skills don't cover (security basics, test health, code hygiene, dependency health, build health). For everything else — model correctness, navigation paths, data safety, visual quality — it consumes findings from the companion skills rather than re-scanning.

## Quick Start

```
/capstone-radar              # Full audit (own scans + companion handoffs)
/capstone-radar quick        # Own domain scans only
/capstone-radar report       # Re-grade from existing handoffs (no scanning)
```

## Three Ways to Use It

### 1. After Companions (Best Coverage)

Run all 4 companion skills first, then capstone for the unified grade. All handoff files exist. Capstone consumes them, adds its own 5 domains, grades everything, gives you the full picture with cross-domain correlation and ship decision.

### 2. Standalone (Start Here)

No handoff files. Capstone runs its own 5 domains, gives you a partial grade, and tells you which companion skills would improve coverage:

```
Coverage gaps — these domains were NOT audited:
  Model Layer: Run data-model-radar for coverage
  Navigation/UX: Run ui-path-radar for coverage
  Data Safety: Run roundtrip-radar for coverage
  Visual Quality: Run ui-enhancer for coverage
```

You still get security, test health, code hygiene, velocity tracking, and risk heatmap.

### 3. Quick Check (Daily Use)

You fixed 3 issues. Run capstone again. It compares to the last run, shows your grade went up, celebrates the improvement, updates velocity tracking. Takes 2-3 minutes. This is the "run it every day" use case.

> Start with capstone-radar to see where you stand. It'll tell you which companion radars to run for deeper coverage. Run those. Then run capstone again for the unified grade and ship decision.

## What It Grades

### Owned Domains (5)

| Domain | What It Checks |
|--------|---------------|
| Code Hygiene | TODO/FIXME/HACK count, `try!`/`as!`, files >1000 lines |
| Test Health | Test file count, test-to-source ratio, Swift Testing vs XCTest, `sleep()` in tests |
| Security Basics | Hardcoded keys/secrets, `http://` URLs, sensitive UserDefaults |
| Dependency Health | Package.resolved age, SPM version constraints, package count |
| Build Health | Scheme count, target count |

### Consumed from Companions (4)

| Source Skill | Domain | What It Gets |
|-------------|--------|-------------|
| data-model-radar | Model Layer | Model grade, migration risks, relationship issues |
| ui-path-radar | Navigation/UX | Navigation grade, dead ends, broken promises |
| roundtrip-radar | Data Safety | Data safety grade, field loss bugs, cross-cutting patterns |
| ui-enhancer | Visual Quality | Visual quality grade, accessibility gaps, color issues |

Plus a **Cross-Domain Risk** domain (5% weight) from correlation analysis.

## Honest Grading

Capstone Radar labels what it actually checked. Every grade includes verification depth (deep-verified / sampled / spot-checked), scope (N/10 domains audited), and a hygiene-only disclaimer when companion domains are missing. It risk-ranks before scanning — directing depth toward areas with prior findings or known asymmetries, not wherever code is easiest to read. It won't produce a clean A+ from surface grep patterns when 45% of weighted domains are unaudited.

## Features

- **Velocity Tracking** — compare grades across runs, see trends, project when you'll hit your target grade
- **Build-Tagged Audits** — tag each audit with build number, compare across releases
- **Celebrate Improvements** — highlights what got better since last run (shown before findings)
- **Risk Heatmap by File** — files appearing in 3+ domains get flagged as concentrated risk
- **Git-Tied Regressions** — new findings traced to the commit that introduced them
- **Test Coverage Gap Analysis** — maps test files to source, flags risky untested code
- **Time-Boxed Fix List** — after ship decision, asks your time budget and prioritizes fixes by grade impact
- **Team Awareness** — auto-detects multi-contributor repos, enriches regressions with PR context, adds ownership to risk heatmap

## Companion Skills (5-Skill Family)

| Skill | Unique Role | GitHub |
|-------|-------------|--------|
| **Data Model Radar** | Are your @Model definitions correct? | [data-model-radar](https://github.com/Terryc21/data-model-radar) |
| **UI Path Radar** | Can users reach every feature? | [ui-path-radar](https://github.com/Terryc21/ui-path-radar) |
| **Roundtrip Radar** | Does data survive the full journey? | [roundtrip-radar](https://github.com/Terryc21/roundtrip-radar) |
| **UI Enhancer** | Does it look and feel right? | [ui-enhancer](https://github.com/Terryc21/ui-enhancer) |
| **Capstone Radar** (this skill) | Can you ship? Unified grade + decision. | [capstone-radar](https://github.com/Terryc21/capstone-radar) |

### How They Work Together

```
data-model-radar  -->  ui-path-radar  -->  roundtrip-radar
 (foundation)          (navigation)        (data flows)
                            |                   |
                            v                   v
                               ui-enhancer
                               (visual quality)
                                     |
                                     v
                              capstone-radar
                              (unified grade + ship/no-ship)
```

### Recommended Audit Order

1. **data-model-radar** first — verify model definitions before auditing flows
2. **ui-path-radar** second — find all entry points and broken paths
3. **roundtrip-radar** third — audit data flows behind those paths
4. **ui-enhancer** fourth — polish views after structural issues are fixed
5. **capstone-radar** last — unified grade and ship/no-ship decision

Capstone is both the **entry point** (what should I audit?) and the **exit point** (can I ship?). The other radars are the deep work in between.

## Installation

```bash
cp SKILL.md ~/.claude/skills/capstone-radar/SKILL.md
```

## License

MIT
