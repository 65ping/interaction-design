# Interaction Design Skill

A Claude skill for interaction design practitioners -> product designers, UX designers, UI designers, service designers, and interaction designers.

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

## What It Does

Activate this skill to get hands-on help with:

- **Interaction flows** — task flows, decision branches, error recovery, exit paths
- **Component states** — all 10 states (default, hover, focus, active, loading, disabled, error, success, empty, skeleton)
- **Micro-interactions** — trigger, rules, feedback, loops and modes
- **Feedback design** — timing, type, and hierarchy based on Nielsen's response-time thresholds
- **Motion and transitions** — duration, easing, when to animate and when not to
- **Affordances and signifiers** — perceived vs actual affordance, drag handles, anti-affordances
- **Mental models** — aligning system behavior with user expectations
- **Interaction specifications** — behavior documentation for handoff
- **Interaction review** — evaluating designs against established principles
- **Role-specific guidance** — for product designers, UX, UI, service designers

## Principles Covered

- Norman's 6 fundamentals (Visibility, Feedback, Constraints, Mapping, Consistency, Affordance)
- Tognazzini's 19 principles
- NNGroup's 8 interactivity attributes
- Nielsen's 3 response-time thresholds
- The 5 dimensions of IxD
- The micro-interaction framework (trigger, rules, feedback, loops)

## Skill Files

```
SKILL.md                        ← main skill (load this)
reference/
  principles.md                 ← full Norman + Tognazzini reference with applied examples
  response-time.md              ← 3 response-time thresholds + all feedback/loading patterns
  patterns-and-flows.md         ← forms, navigation, search, onboarding, errors, empty states, modals, drag-and-drop, gestures
```

## Example Prompts

```
"Help me design the interaction flow for a multi-step checkout"
"What states does this dropdown component need?"
"Review this interaction — does the feedback arrive at the right time?"
"Write an interaction spec for drag-and-drop reordering"
"What's the right animation duration for this modal?"
"How should I handle empty states in this dashboard?"
"I'm a service designer — how do I apply IxD to cross-channel touchpoints?"
```

