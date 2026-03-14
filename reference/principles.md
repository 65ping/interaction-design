# Interaction Design Principles Reference

A complete reference for Norman's 6 fundamentals and Tognazzini's 19 principles,
with applied examples, violation patterns, and design guidance for practitioners.

---

## Norman's 6 Fundamentals

From *The Design of Everyday Things* by Don Norman. These principles apply universally
to any interface — digital, physical, or service.

---

### 1. Visibility

**Definition:** The state of the system and the available actions should be visible.
Users should not have to guess what is happening or what they can do.

**Applied to digital products:**
- Current state is always visible (active nav item highlighted, selected item marked)
- Interactive elements look different from non-interactive ones
- System status is communicated continuously (loading, connected, syncing)

**Violation patterns:**
- A spinner that disappears but the system is still loading
- A menu item that appears but is actually disabled — with no visual distinction
- A recording indicator that is too subtle to notice
- Forms that fail silently

**Design checklist:**
- [ ] Active/selected/current states are clearly indicated
- [ ] Interactive elements are visually distinct from static content
- [ ] System status (loading, saving, syncing, offline) is always communicated
- [ ] Destructive or irreversible states are prominently visible

---

### 2. Feedback

**Definition:** Every user action should produce an immediate, perceivable response.
The system must confirm that it received input and communicate the outcome.

**Timing requirements:**
- 0–100ms: immediate visual state change (button press, toggle flip)
- 100ms–1s: loading indicator
- 1s–10s: progress indicator
- 10s+: background processing with completion notification

**Types of feedback:**
- **Visual**: state change, color shift, animation, icon change
- **Text**: confirmation copy, error message, count update
- **Motion**: transition that communicates what happened and in what direction
- **Haptic**: confirmation tap (native mobile, use sparingly)
- **Audio**: notification chime, error tone (use very sparingly)

**Violation patterns:**
- A form that submits but shows no loading state — user clicks repeatedly
- A delete action with no confirmation — user unsure if it worked
- A file upload with no progress — user cannot tell if transfer is happening
- Success copy that appears for 3 seconds but the user has already scrolled away

**Applied examples:**
- Button: label changes to "Saving..." + spinner on click → "Saved" on success
- Toggle: thumb slides with animation, color shifts, ARIA label updates
- Form field: green checkmark appears on blur when validation passes
- File upload: progress bar fills with percentage

**Design checklist:**
- [ ] Every user action produces visual feedback within 100ms
- [ ] Success and failure states are clearly differentiated
- [ ] Feedback is persistent enough to be noticed (not flashes that disappear)
- [ ] Feedback is proportional — routine actions get subtle feedback; significant actions get prominent feedback

---

### 3. Constraints

**Definition:** Limit the available interactions to only those that are valid in context.
Prevent errors rather than recover from them.

**Types of constraints:**
- **Physical**: a date picker prevents text entry of invalid dates
- **Semantic**: a form only enables "Submit" when required fields are valid
- **Cultural**: a confirm dialog uses conventional button placement for the destructive action

**Applied to digital products:**
- Disable actions that are not available in the current state
- Limit input to valid formats at the field level
- Surface only relevant options in context menus
- Prevent concurrent destructive actions (disable during in-flight request)

**Violation patterns:**
- Allowing free-text for a date field, then showing "invalid date" at submission
- Showing all menu options even when half are unavailable — user tries them and sees errors
- Not disabling a submit button during form processing — user submits twice

**Design checklist:**
- [ ] Invalid actions are disabled, not just error-generating
- [ ] Input constraints are communicated before the user attempts invalid input
- [ ] Context menus and option lists hide or disable unavailable actions
- [ ] Confirmation dialogs clearly identify the destructive action

---

### 4. Mapping

**Definition:** The relationship between controls and their effects should be intuitive.
Controls should spatially or conceptually correspond to what they affect.

**Natural mappings (exploit existing conventions):**
- Scroll up → content moves up (direction matches expectation)
- Volume: left = less, right = more
- Navigation: "Next" on the right, "Back" on the left
- Vertical sliders: up = more, down = less
- Zoom: pinch in = smaller, pinch out = larger

**Violation patterns:**
- A brightness control icon that looks like contrast
- A horizontal slider that decreases in value as it moves right
- Buttons labeled "Yes" / "No" where the desired action is "No" but it is positioned first
- A settings panel that affects a different area of the screen than the user expects

**Special case — button order in destructive dialogs:**
Platform conventions exist specifically because mapping matters here:
- macOS: Cancel (left) → Confirm (right)
- Material Design: Cancel (left) → Confirm (right, outlined) → Destructive (right, filled red)
Deviation from platform convention causes users to confirm destructive actions by accident.

**Design checklist:**
- [ ] Control direction matches effect direction (sliders, scroll, zoom)
- [ ] Destructive actions follow platform conventions for button order
- [ ] Controls are spatially associated with the elements they affect
- [ ] Labels accurately describe what the control does (not just what it is)

---

### 5. Consistency

**Definition:** Similar actions should behave similarly throughout the product. Users
build mental models from patterns — inconsistency causes errors and distrust.

**Levels of consistency:**
1. **Internal**: same component behaves the same everywhere in the product
2. **Platform**: aligns with OS and platform conventions (iOS, Android, Web)
3. **Industry**: aligns with conventions across similar products (Jakob's Law)
4. **Expectation**: matches what users anticipate based on prior experience anywhere

**Applied to digital products:**
- Swipe-to-dismiss works consistently across all lists in the product
- All modals confirm with the same button placement and labeling
- All form validation triggers at the same point (blur vs. submit)
- All destructive actions require the same confirmation pattern

**Violation patterns:**
- Swipe-to-archive in the inbox but swipe-to-delete in the sent folder
- Modals that confirm on the right in some screens, left in others
- One section validates on blur, another validates only on submit
- Different drag-and-drop affordances for visually similar list items

**When to be inconsistent (deliberately):**
Deliberate inconsistency is acceptable when:
- You are correcting a convention that caused harm
- A new interaction pattern provides clear, tested value
- The deviation is signaled and onboarded

**Design checklist:**
- [ ] Component behavior is documented at the system level, not per-screen
- [ ] Interaction patterns are audited across the full product for consistency
- [ ] New interaction patterns are tested before being introduced as a deviation from convention
- [ ] Platform conventions are followed unless there is a documented reason to deviate

---

### 6. Affordance

**Definition:** UI elements should look like they behave. The visual appearance of
a component should communicate how to interact with it.

**Perceived vs. actual affordance:**
- **Actual affordance**: a button can be pressed (capability)
- **Perceived affordance**: the button looks pressable (appearance)
Interaction design is primarily concerned with perceived affordance.

**Signifiers** — explicit signals that communicate how to interact:
- Underline signals "this is a link"
- Border and padding signals "this is a button"
- Drag handle icon signals "this is draggable"
- Dotted border on empty area signals "content can be dropped here"

**Anti-affordances** — signals that something cannot be done:
- Greyed text and reduced opacity signal "this is disabled"
- Lock icon signals "this requires permission"
- `cursor: not-allowed` signals "this action is not available"

**Violation patterns:**
- Flat text that is actually a link — no visual signal of interactivity
- A card that is clickable but has no hover state, cursor change, or affordance signal
- A textarea that looks like static text — no border, no background distinction
- An icon-only button with no tooltip — user cannot determine the action

**Design checklist:**
- [ ] Every interactive element has a distinct visual style from non-interactive elements
- [ ] Draggable and droppable areas have explicit signifiers
- [ ] Disabled elements use anti-affordance signals (opacity, cursor, color)
- [ ] Icon-only buttons have accessible labels and tooltips
- [ ] Perceived affordance is tested with users, not assumed by designers

---

## Tognazzini's 19 Principles

From Bruce Tognazzini's *First Principles of Interaction Design* at AskTog.
These expand Norman's fundamentals into a broader operational framework.

---

### 1. Anticipation

Bring users the information and tools they need at each step, without requiring them to
search elsewhere.

**Application:**
- Pre-fill known data (shipping address, account details, previous selections)
- Surface related actions contextually at the point of need
- Warn before a point of no return in a flow
- Auto-complete based on user history and context

**Examples:**
- Checkout: billing address auto-fills from shipping address
- Compose: recipient suggestions appear as user types
- Delete: "This will permanently delete 23 items" before the user confirms

---

### 2. Autonomy

Users need to feel in control. Design within constraints the user can understand and override.

**Application:**
- Allow customization of defaults and preferences
- Never take irreversible action without explicit user confirmation
- Provide clear status so users understand system state
- Give users the ability to undo or reverse actions

**Warning:**
Autonomy does not mean anything-goes. Systems must maintain some control (preventing
data corruption, maintaining security). The balance is: users feel they are making decisions,
not that the system is making decisions for them.

---

### 3. Consistency

*(See Norman #5 above — these principles converge significantly.)*

Tognazzini adds: consistency with user expectations often matters more than internal
or platform consistency. Users arrive with expectations from all their prior product
experience. Design to match those first.

---

### 4. Defaults

Defaults should represent the best choice for most users in most situations.

**Good defaults:**
- Represent the most common case, not the safest technical choice
- Are easy to override with a clear path to do so
- Use meaningful labels — not "Option A" or "Standard"
- Reduce friction for the majority without restricting the minority

**Default selection patterns:**
- Pre-selected option in a radio group
- Pre-populated form fields from user history
- Default sort order (most recent, most relevant)
- Default time zone from device locale

**Anti-patterns:**
- Defaults that serve the business (opt-in to marketing, maximum plan selected)
- Defaults labeled "Recommended" when they are actually the most expensive
- No clear indication of which option is the default

---

### 5. Discoverability

If users cannot find it, it does not exist. Controls should be visible and accessible
without requiring documentation or prior knowledge.

**Progressive disclosure (not hiding):**
The solution to complexity is progressive disclosure — surfacing advanced features after
basic use is established — not hiding features entirely.

- Primary navigation surfaces the 80% use case
- Secondary navigation or contextual menus surface advanced actions
- Help systems guide users to features, not replace them

**Discoverability at feature launch:**
- Coach marks and tooltips for new features at first encounter
- Empty states that show what the feature does and how to start
- In-product help that guides, not just documents

---

### 6. Efficiency of the User

Optimize for the user's time, not the system's performance metrics. Common tasks must
be fast and direct.

**Application:**
- Keyboard shortcuts for actions used more than once a day
- Bulk operations for repeat actions
- Confirmation dialogs only for high-stakes actions (not routine ones)
- Single-click primary actions — not multi-step confirmation for common tasks

**Anti-patterns:**
- Requiring two clicks to perform the most-used action in the product
- Confirmation dialog for every delete, even when undo is available
- No keyboard shortcuts in a product with power users

---

### 7. Explorable Interfaces

Users should be able to explore without fear. Support exploration through reversibility.

**Application:**
- Undo for all destructive or modifying actions (CMD+Z / system-level undo)
- Preview before commit (image crop, document format, color selection)
- Breadcrumbs and clear back navigation
- Warn before unsaved changes are lost

**Not the same as discoverability:**
Explorable ≠ discoverable. Explorable means users can safely try things.
Discoverable means users can find things.

---

### 8. Fitts's Law

The time to acquire a target is a function of its distance from the cursor and its size.

**Formula (simplified):** MT = a + b × log₂(D/W + 1)
- MT = movement time
- D = distance to target
- W = width of target

**Practical application:**

| Context | Minimum target size |
|---|---|
| Touch (iOS) | 44×44pt |
| Touch (Android / Material) | 48×48dp |
| Mouse (desktop web) | 32×32px |
| Small text links (desktop) | At least 24px height |

- Primary CTAs should be the largest interactive element in the viewport area
- Place frequent actions close together (related actions ≤200px apart)
- Screen edges are "infinite" targets in one direction — use them for navigation and system controls
- Minimize the number of targets the user must acquire to complete a task

---

### 9. Latency Reduction

Acknowledge every user action within 100ms, regardless of how long the processing takes.

**Implementation:**
- Disable the button immediately on click (prevents duplicate submissions)
- Show a spinner or state change within 100ms
- For long operations: show estimated time remaining
- Use optimistic UI for high-confidence operations

**Background processing pattern:**
When an operation takes more than 10 seconds:
1. Tell the user the operation is running in the background
2. Allow them to continue using the product
3. Notify them (push notification, email, in-app toast) when complete

---

### 10. Learnability

Interfaces should be learnable over time. Expert use should be significantly faster
and more efficient than first use.

**Design for expertise:**
- Keyboard shortcuts for frequent actions
- Command palettes (CMD+K) for power users
- Contextual menus that reveal advanced options
- Customizable workflows and shortcuts

**Learnability vs. discoverability tension:**
Highly learnable interfaces (keyboard-driven, shortcut-heavy) are often less discoverable.
Resolve by: discoverable first, efficient after experience.

---

### 11. Metaphors

Metaphors help users map new systems onto existing mental models. Choose them carefully.

**Good metaphor criteria:**
- Accurately conveys the core behavior (not just the name)
- Does not imply constraints that do not exist
- Is recognizable across cultures and demographics
- Does not limit future evolution of the feature

**Overextended metaphors to avoid:**
- Desktop/folder/file metaphors in cloud-native products where files do not work that way
- "Inbox" metaphor for notification feeds where the inbox contract (empty = done) does not apply
- Physical trash can where deleted items are actually permanently gone immediately

---

### 12. Protect the User's Work

Never destroy user-generated content due to interface errors, navigation, or unexpected input.

**Implementation:**
- Auto-save at regular intervals (every 30 seconds for text input, on every change for form state)
- Warn before navigating away from unsaved state: "Leave page? Changes you made may not be saved."
- Never clear a form on validation failure — preserve all entered values
- Provide undo for all destructive actions within a reasonable window (30 seconds to 30 days depending on action significance)

---

### 13. Readability

Text must be legible for the full range of users, not ideal conditions only.

**Minimum standards:**
- Body text: 16px (web), 15–17pt (iOS), 14–16sp (Android)
- Contrast: 4.5:1 for normal text (WCAG AA), 3:1 for large text (18pt+ or 14pt+ bold)
- Line length: 50–75 characters for prose, up to 90 for data-dense UI
- Line height: 1.4–1.6 for body text
- Typefaces: use proven readable faces at body size; reserve display faces for headings

**Test in degraded conditions:**
- Bright sunlight on mobile
- Small screen with default OS text scaling
- Users over 50 (reduced contrast sensitivity, need larger text)

---

### 14. Simplicity

Simplicity means reducing unnecessary complexity, not removing functionality.

**Progressive revelation vs. removal:**
- Progressive revelation: hide advanced controls until the user needs them
- Removal: eliminate features entirely because they are complex

Progressive revelation maintains simplicity while preserving power.
Removal creates products that are simple to start but limited to grow.

**Apparent simplicity vs. actual simplicity:**
A product with 3 settings but poor information architecture is not simple.
A product with 30 settings organized into a clear, searchable hierarchy can feel simple.

---

### 15. State

Track and restore meaningful state across sessions.

**What to preserve:**
- Scroll position
- Form in progress (auto-save)
- Panel open/closed state
- Tab selection
- Sort/filter settings for data tables
- Search history

**What to indicate:**
- Current location in navigation (active state)
- New vs. visited content
- Unread counts and notification badges
- Sync status (saved, saving, offline)

---

### 16. Visible Navigation

Users must always know where they are, where they can go, and how to get back.

**Navigation visibility requirements:**
- Current location highlighted in navigation (active state with accessible label)
- Breadcrumbs for hierarchies deeper than 2 levels
- Back button works as expected — goes to the previous state, not the previous URL
- Search is always accessible (not buried in secondary navigation)

**Dead-end prevention:**
Every screen must have a clear path out. Even error pages need navigation.
Never trap users in a modal that cannot be dismissed without completing the action.

---

### 17. Aesthetics

Visual design influences perceived usability. Aesthetic quality signals care and quality.

**The aesthetic-usability effect:**
Users rate attractive interfaces as more usable, even when usability is identical.
This builds tolerance for minor friction.

**The limit:**
Aesthetic quality cannot compensate for fundamental interaction failures.
An unusable product with beautiful visuals is still unusable.

---

### 18. Color

Color communicates meaning. Design for users who cannot rely on color alone.

**Color accessibility:**
- 8% of males and 0.5% of females have some form of color vision deficiency
- Red-green color blindness is the most common — never rely on red/green alone for status
- Use color + shape + label as triple redundancy for critical states

**Color semantics (web convention):**
- Red: error, destructive, critical
- Yellow/amber: warning, in-progress, caution
- Green: success, safe, active
- Blue: information, link, selected, interactive

**When to use red:**
Only for error and destructive actions. Red on a neutral action (e.g., a standard navigation button) violates user expectation and signals danger where none exists.

---

### 19. Human-Interface Objects

Interactive objects should behave consistently regardless of where they appear.

**Stable object behavior:**
A button is a button. It is perceivable, can be clicked, responds to pointer and keyboard,
and produces a consistent, expected result. Every button in the product should behave
this way — not some buttons some of the time.

**Consistency of affordance:**
The visual appearance of an object signals its interaction capability.
An object that looks like a button but does not behave as a button (does not respond to
hover, does not show a loading state, does not produce feedback) violates this principle.

---

*Last updated: 2026. Sources: Norman (2013), Tognazzini (AskTog), Nielsen Norman Group.*
