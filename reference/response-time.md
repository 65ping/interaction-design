# Response Time and Feedback Patterns

Reference for Nielsen's three response-time thresholds and their implementation
in digital products. Use this to decide which feedback mechanism to use and when.

---

## The Three Thresholds

Jakob Nielsen's research, originally published in *Usability Engineering* (1993) and
confirmed by decades of HCI research, establishes three fundamental response-time limits
based on human perception:

| Threshold | Time | Perception | Required Response |
|---|---|---|---|
| **Instantaneous** | 0 – 100ms | Feels direct; delay not perceived | Visual state change on the element |
| **Flow maintained** | 100ms – 1s | User notices but stays focused | Loading indicator (spinner or skeleton) |
| **Attention limit** | 1s – 10s | User must consciously maintain focus | Progress indicator with time estimate |
| **Abandonment risk** | > 10s | Users disengage, often leave | Background processing + completion notification |

### Why These Numbers

The thresholds are not arbitrary — they map to human perceptual limits:

**100ms** — the limit of "immediate response." Above this, users perceive a gap between
action and effect. Below it, the interface feels physically responsive (like pressing a
physical button).

**1 second** — the limit of uninterrupted attention flow. Users can tolerate this delay
without losing their train of thought, but they notice it. Above 1 second, users need
something to look at to maintain engagement.

**10 seconds** — the limit of sustained attention on a single task. Users typically switch
context, start a new task, or leave the product entirely. Web pages have the lowest
tolerance; native apps and complex tools have slightly higher tolerance when context is clear.

---

## 0–100ms: Instantaneous Response

### What to show
A visual state change on the element that received the interaction. No spinner needed.
No loading copy needed. Just an immediate signal that the element received the input.

### Patterns

**Button active state**
```
Default → Active (pressed appearance: shadow removed, slight scale, color darken) → [100ms] → Loading or success state
```

**Toggle flip**
```
Tap → Thumb slides immediately with animation → Color shifts → ARIA state updates
```
Duration: 100–150ms for the flip animation itself.

**Checkbox check**
```
Click → Checkbox fills with checkmark immediately → (If async) fills with spinner overlay
```

**Text input focus**
```
Click/tap → Border highlights immediately → Cursor appears
```

### Key principle
The visual state change must happen synchronously on the main thread. If JavaScript is
blocking the main thread, the browser cannot render the state change within 100ms. This
is why button states that depend on JavaScript events feel "laggy" — optimize rendering
performance to keep the interaction thread free.

---

## 100ms–1s: Spinner or Skeleton

### What to show
A loading indicator that tells the user the system is processing. At this duration,
a simple spinner is acceptable. For content-loading scenarios, a skeleton screen is better.

### Choosing between spinner and skeleton

**Use a spinner when:**
- The result will be a single, small element (a count, a status, a boolean)
- The result will replace the entire screen (navigate to new page)
- The action is a command, not a data load (save, delete, send)

**Use a skeleton when:**
- The result will be a complex layout (list of cards, a feed, a table)
- The user is loading a page or section for the first time
- Content will appear in a predictable structure you can approximate

**Why skeletons beat spinners for content:**
- Skeletons reduce perceived wait time by showing layout structure immediately
- They prevent layout shift (content jumping into position)
- They give the eye something to anchor on while waiting
- They feel faster than an equivalent spinner even at identical load times (per research)

### Spinner patterns

**Button spinner (action in progress)**
```
Button label: "Save document"
After click: Spinner replaces label icon, text changes to "Saving..."
Disabled state: true
On success: "Saved" with checkmark, re-enables after 1.5s
On error: Error icon, text changes to "Save failed — try again", re-enables
```

**Inline spinner (partial UI update)**
```
Component shows spinner overlay while data refreshes
Surrounding UI remains interactive
Width/height preserved to prevent layout shift
```

**Full-page spinner (navigation)**
```
Use sparingly — prefer skeleton screens
Acceptable for initial app load or very fast transitions
Avoid for page-to-page navigation where skeleton is possible
```

### Skeleton patterns

**List skeleton**
```
3–5 skeleton rows, each approximating:
- Avatar circle (gray, correct size)
- Title line (gray, 60–80% width)
- Subtitle line (gray, 40–60% width)
- Shimmer animation passes left-to-right on a 1.5s loop
```

**Card skeleton**
```
Card shell (full dimensions, correct aspect ratio)
Image placeholder (full width, gray)
Title line, subtitle line, body lines
Shimmer on a 1.5s loop
```

**Dashboard skeleton**
```
Match the actual dashboard layout exactly — header, sidebar, main content area, cards
Use correct grid proportions
Shimmer across all elements simultaneously
```

**Shimmer animation:**
```css
@keyframes shimmer {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

.skeleton {
  background: linear-gradient(
    90deg,
    #e0e0e0 25%,
    #f0f0f0 50%,
    #e0e0e0 75%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}
```

---

## 1s–10s: Progress Indicator

### What to show
A progress indicator that communicates:
1. The action is still running (system has not crashed)
2. How far along the operation is (if deterministic)
3. Estimated time remaining (if available)

### Deterministic vs. indeterminate

**Deterministic** — you know progress: use a progress bar with percentage.

```
File upload: 47% ■■■■■■■■░░░░░░░░░  "Uploading... 3.2 MB of 6.8 MB"
```

**Indeterminate** — you do not know progress: use an animated indicator (not a spinner
if the user will be waiting more than 3 seconds — spinners become anxiety-inducing).

```
Generating report: ■■■■■■■░░░░░░░░░░  "Processing data..."
```

For indeterminate operations over 3 seconds, consider a pulsing progress bar that moves
but does not indicate percentage — more calming than an infinite spinner.

### Progress bar patterns

**File upload / download**
```
Progress bar (filled portion = % complete)
Text: "3.2 MB of 6.8 MB — 47%"
Secondary text: "~12 seconds remaining" (if calculable from transfer rate)
Cancel button: allows user to abort
```

**Multi-step operation (database migration, bulk action)**
```
Step indicator: "Step 2 of 5: Validating data..."
Progress bar: 40% (2/5 steps)
Substep progress: "Processing record 2,341 of 5,000"
```

**Batch processing**
```
"Processing 247 of 1,000 items"
Progress bar: 24.7%
Option to run in background (see 10s+ pattern)
```

### Copy guidelines for progress states

**Do:**
- Say what is happening: "Uploading file", "Generating report", "Processing payment"
- Show time remaining when calculable: "About 45 seconds remaining"
- Show count/progress when available: "47 of 200 items processed"

**Do not:**
- Show generic "Loading..." for operations over 3 seconds
- Show a percentage that never moves (stuck progress bars destroy trust)
- Show "Almost done..." for longer than 3 seconds (users stop believing it)

---

## 10s+: Background Processing

### What to show
For operations expected to take more than 10 seconds, move to background processing.
Tell the user, let them continue working, and notify them on completion.

### Background processing pattern

**Step 1: Initiate and inform**
```
User triggers operation
→ System immediately: moves operation to background, shows confirmation toast
Toast: "Your report is generating. We'll notify you when it's ready."
User can continue using the product normally
```

**Step 2: Persist state visibility**
```
Show a background jobs indicator (bell icon badge, status bar, jobs panel)
User can check progress at any time without being blocked
```

**Step 3: Notify on completion**
```
In-product notification: "Your Q3 Sales Report is ready. [View Report]"
Optional: email notification for very long operations (>5 minutes)
Optional: push notification for mobile
```

**Step 4: Handle failure**
```
In-product notification: "Report generation failed. [Retry] [Contact support]"
Never silently fail a background operation
```

### When to use background processing
- Report generation (>10s)
- Large file exports or imports
- Batch operations on >100 items
- Any ML/AI inference that takes more than a few seconds
- Email or message sending (optimistic UI, background confirmation)
- Video/image processing

### Background job UI patterns

**Jobs status panel (sidebar or dropdown)**
```
[Active Jobs]
■■■■░░░░ Exporting contacts (67%)  [Cancel]
[Completed]
✓ Report generated — 2 minutes ago  [Download]
✓ 250 contacts imported — 5 minutes ago
```

**Notification bell badge**
```
Bell icon in header
Badge: number of new completed jobs
Clicking opens jobs panel or notification list
```

---

## Optimistic UI

### When to use
Optimistic UI applies the result of an action immediately in the UI before server
confirmation, then rolls back if the server returns an error.

**Use when:**
- The operation is very likely to succeed (>99% expected success rate)
- The operation is reversible (like, follow, upvote, add to list)
- The latency overhead is not worth the visual cost of waiting

**Do not use when:**
- The operation has significant failure scenarios (payment, file save, data migration)
- The operation is irreversible (delete, publish, send)
- Failure would require complex UI state reconciliation

### Optimistic UI pattern

```
User taps "Like"
→ Heart fills immediately (optimistic state applied)
→ Count increments immediately
→ API call fires in background
→ On success: nothing changes (already correct)
→ On failure: heart unfills, count decrements, toast: "Couldn't save. Try again."
```

### Rollback patterns
When the optimistic action fails, the rollback must:
1. Restore the previous UI state visually
2. Inform the user that the action did not succeed
3. Offer a clear retry path

---

## Perceived Performance Techniques

Beyond actual speed, these techniques improve how fast the interface feels:

### Instant transitions
The fastest-feeling transition is one that appears instant. For operations that are
genuinely fast (<50ms), skip the transition entirely. Fade-ins and slide-ins add
perceived latency even when they make the UI look polished.

### Pre-fetching
Load content before the user navigates to it:
- Prefetch on hover (web): start loading the destination page when the cursor hovers a link
- Prefetch on visible (mobile): load offscreen items in a list
- Prefetch on intent: predict the next likely action and pre-load it

### Optimistic navigation
Navigate to the new screen immediately, then load content within the destination.
The skeleton screen shows instantly; content populates progressively.
This is faster-feeling than waiting for data before rendering the new screen.

### Progressive image loading
Low-quality image placeholder (LQIP) → full image loads in
- LQIP: a blurred 20px version of the image, inlined as base64
- Full image fades in over the LQIP as it loads
- User sees content structure immediately, not a grey box

---

## Feedback Type Decision Matrix

| Action | Duration | Feedback Type |
|---|---|---|
| Button click (fast API) | <500ms | Button state change → success/error state |
| Form submit | 500ms–2s | Button spinner → form success or inline errors |
| File upload (small) | 1–5s | Progress bar with percentage |
| File upload (large) | 5–30s | Progress bar + time estimate + cancel option |
| Report generation | 10–60s | Background job + notification |
| Bulk data import | 30s–5min | Background job + email notification |
| Toggle / like / follow | <200ms | Optimistic UI (immediate state change) |
| Delete (undo available) | <200ms | Optimistic UI + undo toast |
| Delete (permanent) | <500ms | Confirmation first → spinner → success state |
| Page navigation | <1s | Skeleton screen |
| Search results | 200ms–2s | Skeleton rows or spinner in results area |
| Auto-save | Background | Subtle status indicator ("Saving..." → "Saved") |

---

*Sources: Nielsen (1993, 2010), Miller (1968 — the original response time study),
Card, Moran & Newell (1983), NNGroup.*
