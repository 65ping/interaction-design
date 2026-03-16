<div align="center">

<br/>

```
  ◈ AUDIT → ANALYSE → SPECIFY → HANDOFF ◈
```

# Interaction Design
### A Claude Code Skill

**Principled interaction design, from behaviour mapping to engineering handoff.**
Built for product designers, UX designers, UI designers, service designers, and interaction designers.

<br/>

[![Version](https://img.shields.io/badge/version-1.0.0-0a0a0a?style=flat-square&labelColor=f5f0e8)](https://github.com/65ping/interaction-design-skill)
[![Dimensions](https://img.shields.io/badge/dimensions-5-0a0a0a?style=flat-square&labelColor=f5f0e8)](https://github.com/65ping/interaction-design-skill/blob/main/SKILL.md)
[![Principles](https://img.shields.io/badge/principles-19-0a0a0a?style=flat-square&labelColor=f5f0e8)](https://github.com/65ping/interaction-design-skill/blob/main/SKILL.md)
[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-0a0a0a?style=flat-square&labelColor=f5f0e8)](https://claude.ai/claude-code)

<br/>

</div>

---

## Install

**Add to an existing Claude Code project:**

```bash
# Clone into your project's .claude/skills directory
git clone https://github.com/65ping/interaction-design-skill.git .claude/skills/interaction-design
```

**Or install globally** (available across all your projects):

```bash
git clone https://github.com/65ping/interaction-design-skill.git ~/.claude/skills/interaction-design
```

Claude Code will detect the skill automatically. No configuration needed.

---

## What It Does

This skill turns Claude into an interaction design practitioner: auditing flows, specifying states, defining timing, and producing handoff-ready documentation. Tell Claude what you're designing and where you're stuck. It adapts to your role, phase, and output needs.

```
"What states does this toggle switch need?"
"Map the interaction flow for a multi-step checkout including all error paths"
"How long should a loading skeleton show before switching to an error state?"
"Write an interaction spec for drag-and-drop reordering I can give to engineering"
"I'm a service designer. How do I apply interaction design across a patient journey?"
```

Claude responds with structured flows, state tables, timing specs, or annotated documentation, grounded in established principles.

---

## The Five Dimensions

| # | Dimension | Core Question | Output |
|---|---|---|---|
| 1 | 📝 **Words** | Does the language guide without creating confusion? | Labels, instructions, error copy, microcopy |
| 2 | 👁️ **Visual Representations** | Do icons, imagery, and layout communicate state clearly? | Affordances, signifiers, visual feedback |
| 3 | 🖐️ **Physical Objects & Space** | How does device context and environment shape interaction? | Hardware constraints, spatial mapping, gesture design |
| 4 | ⏱️ **Time** | Does feedback arrive exactly when users expect it? | Timing specs, transitions, loading and skeleton states |
| 5 | 🔁 **Behaviour** | Does the system respond the way users predict it will? | State machines, flows, rules, error recovery paths |

> Most interaction failures trace back to a single neglected dimension. Diagnosing which one is half the fix.

---

## Who It's For

### 🖥️ Product & UX Designers
Product designers and UX designers defining how a product behaves end-to-end, from onboarding to error recovery to empty states.

- Maps full task flows with entry points, decision branches, and exit paths
- Defines all 10 component states so nothing gets left to developer interpretation
- Produces interaction specifications formatted for engineering handoff

### 🎨 UI & Visual Designers
UI designers specifying the detail layer: component behaviour, motion, timing, and micro-interactions that separate good interfaces from great ones.

- Specifies animation duration, easing curves, and motion intent
- Documents micro-interactions using the trigger → rules → feedback → loops framework
- Flags affordance and signifier gaps before they become usability failures

### 🔄 Service & Systems Designers
Service designers and systems thinkers applying interaction design principles across touchpoints: digital, physical, and in-person.

- Adapts interaction design principles to cross-channel journeys
- Identifies where experience breaks down between touchpoints
- Frames interaction quality as a service-level concern, not a screen-level one

---

## What's Inside

```
interaction-design/
│
├── SKILL.md                          ← Main skill file (auto-loaded by Claude Code)
│   ├── 5 Dimensions of Interaction   ← Words, visual, physical, time, behaviour
│   ├── Norman's 6 Fundamentals       ← Visibility, feedback, constraints, mapping, consistency, affordance
│   ├── Tognazzini's 19 Principles    ← Anticipation, autonomy, defaults, efficiency, and more
│   ├── Component states (all 10)     ← Default, hover, focus, active, loading, disabled, error, success, empty, skeleton
│   ├── Response-time thresholds      ← ≤100ms, ≤1s, ≤10s, with guidance on what to show at each
│   ├── Micro-interaction framework   ← Trigger, rules, feedback, loops and modes
│   ├── Motion and transitions        ← Duration, easing, when to animate and when not to
│   ├── Role-specific guidance        ← Product / UX / UI / service designer paths
│   └── Anti-patterns                 ← Common interaction failures organised by dimension
│
└── reference/
    ├── principles.md                 ← Full Norman + Tognazzini reference with applied examples
    ├── response-time.md              ← 3 thresholds + all feedback, loading, and skeleton patterns
    └── patterns-and-flows.md        ← Forms, navigation, search, onboarding, errors, empty states, modals, drag-and-drop, gestures
```

---

## Prompt Examples

The most effective way to use this skill is to describe what you're designing and what you need. Claude handles the rest.

---

### Simple: Single principle or state lookup

**Get all component states:**
```
What states does a primary button need?
List all of them and describe what triggers each one.
```
→ Claude returns all 10 states (default, hover, focus, active, loading, disabled, error, success, empty, skeleton) with trigger conditions and visual behaviour notes for each.

**Check feedback timing:**
```
How long should a loading skeleton show
before switching to an error state?
```
→ Claude applies the three response-time thresholds, returns the correct timing with rationale, and recommends what to show the user at each stage.

**Evaluate an affordance:**
```
Is a chevron icon alone enough to signal
that a list item is expandable?
```
→ Claude diagnoses whether the affordance is perceived or only actual, flags the signifier gap, and suggests what to add.

**Pick the right animation:**
```
Should a modal fade in, slide in, or scale in?
We're designing a confirmation dialog on mobile.
```
→ Claude recommends the motion pattern that matches the spatial metaphor, with duration and easing values.

---

### Intermediate: Flow or pattern design

**Map a complete flow:**
```
I'm designing a password reset flow.
Map the full interaction: every state, every branch,
every error condition, and the success path.
```
→ Claude returns an annotated flow with every state labelled, error paths documented, and re-entry points called out.

**Design an onboarding interaction:**
```
I'm designing onboarding for a B2B SaaS tool
aimed at operations managers who are not technical.
What interaction patterns should I use to guide
first-time setup without overwhelming them?
```
→ Claude recommends patterns matched to the audience's mental model, with progressive disclosure principles applied and anti-patterns flagged.

**Audit for interaction problems:**
```
Here's our checkout flow: [paste flow or describe steps].
Flag every interaction anti-pattern you can find.
I'm especially worried about error recovery and feedback timing.
```
→ Claude runs the flow against Norman's fundamentals and the five dimensions, returns ranked issues with severity, and suggests specific fixes.

**Specify a micro-interaction:**
```
Write the full micro-interaction spec for a
"save draft" action in a form builder tool.
Include trigger, rules, feedback, and loop behaviour.
```
→ Claude returns a complete spec using the trigger → rules → feedback → loops framework, formatted for handoff.

---

### Complex: Full specification or cross-system design

**Full flow spec for engineering handoff:**
```
I'm redesigning the money transfer flow in a mobile banking app.
Map the complete interaction: every step, edge case, error state,
empty state, loading moment, and success feedback.
Format the output as an interaction spec I can hand
directly to my engineering team.
```
→ Claude returns a structured spec with flows, state tables, feedback timing, error recovery paths, and copy guidance, formatted for developer handoff without ambiguity.

**Component state system for a design system:**
```
We're building a design system for a healthcare platform.
Define the full interaction behaviour for our form components:
text input, dropdown, date picker, and file upload.
Include all states, transitions, error handling,
and accessibility behaviour for each.
```
→ Claude produces a component-by-component state specification with interaction rules, ARIA state notes, and transition logic for each component.

**Service designer: apply IxD across touchpoints:**
```
I'm a service designer working on a hospital patient journey
that spans a mobile app, a check-in kiosk, and an in-person
consultation with a nurse. Apply interaction design principles
across all three touchpoints. Where do the principles hold,
where do they break down, and where is the experience
most likely to fail between channels?
```
→ Claude maps interaction quality across each touchpoint, identifies where the five dimensions conflict between channels, and flags the highest-risk handoff moments in the journey.

**Redesign with constraint: tight deadline:**
```
We're three days from a development handoff and we just
discovered our error states are completely undefined.
We have a 12-screen flow. What's the minimum interaction
design work we need to do before handoff, in what order,
and what can we defer safely?
```
→ Claude returns a triage plan prioritising critical error paths, a minimum viable state spec for each screen, and a clear list of what to document in a follow-up sprint.

---

## The Interaction Triangle

Every interaction design decision balances three questions:

- **Behaviour:** Does the system respond the way the user predicts it will?
- **Feedback:** Does the user know what happened, what's happening, and what to do next?
- **Timing:** Does that feedback arrive at the moment it's needed, not too early and not too late?

When all three align, the interaction disappears. The user just gets things done.

---

<div align="center">

Built as a [Claude Code](https://claude.ai/claude-code) skill · v1.0.0

</div>
