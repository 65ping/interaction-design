# Interaction Design Skill Overview

This Claude Code skill applies interaction design principles to real product, UX, UI, and service design challenges. It's built around the five dimensions of interaction and two foundational frameworks — giving designers a structured, principled way to evaluate, specify, and improve how products behave.

## Install

```bash
git clone https://github.com/65ping/interaction-design ~/.claude/skills/interaction-design
```

Or with the GitHub CLI:

```bash
gh repo clone 65ping/interaction-design ~/.claude/skills/interaction-design
```

Claude Code picks up skills automatically from `~/.claude/skills/`. No restart needed — the skill is available immediately in any project.

**Update to latest:**
```bash
git -C ~/.claude/skills/interaction-design pull
```

**Uninstall:**
```bash
rm -rf ~/.claude/skills/interaction-design
```

---

## Core Framework

The skill anchors on the **5 Dimensions of Interaction** — words, visual representations, physical objects and space, time, and behaviour. As a guiding principle: *"If any dimension is neglected, the interaction fails."* These dimensions are cross-referenced with two foundational systems: **Norman's 6 Fundamentals** (visibility, feedback, constraints, mapping, consistency, affordance) and **Tognazzini's 19 Principles** (anticipation, autonomy, defaults, efficiency, and more). Together, they form a complete diagnostic and generative system for interaction problems.

## How It Works

1. **Interaction Audit** — maps task flows, entry and exit points, decision branches, and flags every missing component state or feedback gap
2. **Gap Analysis** — classifies failures by dimension: wrong timing, missing affordance, unclear feedback, broken mapping, or inconsistent behaviour
3. **Specification** — produces annotated interaction flows, component state tables, motion and timing guidelines, and micro-interaction rules ready for handoff

## Intended Users

The skill is built for product designers, UX designers, UI designers, service designers, and dedicated interaction designers. It's especially useful when designing checkout and onboarding flows, defining component state systems, evaluating feedback timing, building design system interaction guidelines, or mapping cross-channel service touchpoints.

## Prompt Examples

**Simple — quick principle or rule lookup:**
> "What states does a button need?"

> "How long should a loading spinner show before displaying an error message?"

**Medium — flow or pattern design:**
> "I'm designing an onboarding flow for a B2B SaaS tool. What interaction patterns should I use to guide first-time users through setup without overwhelming them?"

> "Review this checkout flow and flag any interaction anti-patterns — I'm especially worried about error recovery."

**Complex — full specification and handoff:**
> "I'm redesigning a mobile banking app. Help me map the complete interaction flow for transferring money between accounts — including all edge cases, error states, empty states, loading moments, and success feedback. Format the output as an interaction spec I can hand directly to my engineering team."

> "I'm a service designer working on a healthcare patient journey that spans a mobile app, a kiosk, and an in-person consultation. Help me identify where interaction design principles apply across each touchpoint and flag where the experience is likely to break down."

## Quality Assurance Layer

Every recommendation is tested against the core dimensions before output: Does the system communicate clearly (words)? Are affordances visible (visual)? Does feedback arrive at the right moment (time)? Does the behaviour match the user's mental model (behaviour)? This prevents recommending interactions that are technically correct but experientially broken.

The skill includes 10 component states, 19 system principles, response-time thresholds, micro-interaction frameworks, and annotated pattern libraries — ready to apply immediately.
