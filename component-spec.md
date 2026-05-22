# DRAD Design System — Component Specification
> Version 1.0 | AI-readable spec for Claude, ChatGPT, Cursor, Copilot

---

## How to use this file

Paste this entire file into any AI tool and say:
> "Using the DRAD design system spec below, build me a [describe your screen]"

The AI will use the exact class names, HTML structure, tokens, and rules defined here.

---

## 1. Setup

Always include these in your HTML `<head>`:

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/dist/tabler-icons.min.css">
<link rel="stylesheet" href="drad-design-system.css">
```

---

## 2. Design Tokens

```css
--primary: #006fcf          /* Brand blue — CTA buttons, links, active states */
--primary-hover: #005eb0
--primary-light: #eaf4fd    /* Tinted background for active/selected states */
--primary-border: #b5d7f4

--success: #00875a           /* Approved, completed, positive */
--warning: #b26a00           /* Pending, caution */
--error: #c9372c             /* Error, rejected, destructive */

--text-primary: #1c1c1e      /* Headings, strong labels */
--text-secondary: #3c3c3c    /* Body text */
--text-muted: #666666        /* Supporting text */
--text-disabled: #8c8c8c     /* Labels, captions, placeholders */

--surface-page: #ffffff
--surface-subtle: #f9fafb    /* Alternate rows, panel backgrounds */
--border: #d1d1d1
--border-light: #e5e7eb

--font: 'Inter', system-ui, sans-serif
--font-size-base: 16px
--btn-height: 48px           /* Default button height */
--btn-radius: 8px
--input-height: 48px
--input-radius: 8px
--card-radius: 8px
```

---

## 3. Typography

### Classes
- `.text-display` — 28px bold. Page titles only.
- `.text-heading`  — 22px bold. Section headings.
- `.text-subhead`  — 18px semibold. Subsections.
- `.text-body`     — 16px regular. All general content.
- `.text-sm`       — 12px muted. Supporting text.
- `.text-xs`       — 11px disabled. Captions, labels.
- `.text-label`    — 11px uppercase bold with letter-spacing. Column headers, section labels.

### Rules
- Always sentence case. Never ALL CAPS or Title Case on body text.
- Label text (`.text-label`) is the only exception — it uses uppercase.
- Use `--text-primary` for headings, `--text-secondary` for body, `--text-disabled` for captions.

---

## 4. Buttons

### HTML
```html
<!-- Primary (submit, confirm, main CTA) -->
<button class="btn btn-primary">Submit</button>

<!-- Secondary (save draft, secondary action) -->
<button class="btn btn-secondary">Save draft</button>

<!-- Danger (delete, irreversible action) -->
<button class="btn btn-danger">Delete</button>

<!-- Ghost (cancel, dismiss) -->
<button class="btn btn-ghost">Cancel</button>

<!-- Small variant — add btn-sm to any -->
<button class="btn btn-primary btn-sm">Submit</button>

<!-- With icon -->
<button class="btn btn-primary"><i class="ti ti-send" aria-hidden="true"></i>Submit</button>

<!-- Disabled -->
<button class="btn btn-primary" disabled>Submit</button>
```

### Rules
- Use `btn-primary` for the single most important action per screen.
- Use `btn-danger` only for destructive/irreversible actions.
- Never use `btn-primary` for cancel or navigation — use `btn-ghost`.
- Always put icon before label text.
- One primary button per form/modal at most.

---

## 5. Input Fields

### HTML
```html
<!-- Standard field -->
<div class="field">
  <label class="field-label">Email address <span class="field-req">*</span></label>
  <input type="email" placeholder="you@company.com">
  <span class="field-hint">We'll never share your email.</span>
</div>

<!-- Error state -->
<div class="field">
  <label class="field-label">Email address</label>
  <input type="email" class="input-error" value="invalid@">
  <span class="field-error"><i class="ti ti-alert-circle"></i> Enter a valid email address</span>
</div>

<!-- Disabled -->
<input type="text" value="Read only value" disabled>

<!-- Textarea -->
<div class="field">
  <label class="field-label">Message</label>
  <textarea placeholder="Enter your message..."></textarea>
</div>

<!-- Select / Dropdown -->
<div class="field" style="position:relative">
  <label class="field-label">Request type</label>
  <select>
    <option>Suppression</option>
    <option>Extraction</option>
  </select>
  <i class="ti ti-chevron-down" style="position:absolute;right:12px;bottom:14px;pointer-events:none;color:var(--text-disabled)"></i>
</div>
```

### Rules
- Always wrap inputs in `.field` with a `.field-label`.
- Required fields get `<span class="field-req">*</span>` after the label.
- Error state uses `.input-error` class + `.field-error` message below.
- Hint text uses `.field-hint` — appears below input in default state.

---

## 6. Checkbox

```html
<label class="checkbox">
  <input type="checkbox">
  <div class="checkbox-box">
    <!-- checkmark rendered via CSS when checked -->
  </div>
  <span class="checkbox-label">Option label</span>
</label>
```

---

## 7. Radio Button

```html
<label class="radio">
  <input type="radio" name="group">
  <div class="radio-ring"></div>
  <span class="radio-label">Option label</span>
</label>
```

---

## 8. Chips & Tags

```html
<!-- Chip group (frequency/filter toggles) -->
<div style="display:flex;gap:8px">
  <div class="chip active">One time</div>
  <div class="chip">Weekly</div>
  <div class="chip">Monthly</div>
</div>

<!-- Tag input -->
<div class="tag-input-wrap">
  <span class="tag">A. Patel <button class="tag-close">&times;</button></span>
  <span class="tag">M. Chen <button class="tag-close">&times;</button></span>
  <input placeholder="Add person...">
</div>
```

---

## 9. Badges & Status

```html
<!-- Badge pills -->
<span class="badge badge-green">Approved</span>
<span class="badge badge-blue">In review</span>
<span class="badge badge-amber">Pending</span>
<span class="badge badge-red">Rejected</span>

<!-- Status with dot -->
<span class="status status-success">
  <span class="status-dot"></span>Completed
</span>
<span class="status status-warning">
  <span class="status-dot"></span>In progress
</span>
<span class="status status-error">
  <span class="status-dot"></span>Failed
</span>
```

### Mapping
| State      | Badge class     | Status class      |
|------------|-----------------|-------------------|
| Approved   | badge-green     | status-success    |
| In review  | badge-blue      | status-info       |
| Pending    | badge-amber     | status-warning    |
| Rejected   | badge-red       | status-error      |

---

## 10. Tabs

```html
<div class="tabs">
  <div class="tab active">My Requests</div>
  <div class="tab">All Requests</div>
  <div class="tab">Archive</div>
</div>
```

---

## 11. Cards

```html
<!-- Standard card -->
<div class="card">
  <div class="card-header">Card heading</div>
  <p class="text-body">Card content goes here.</p>
</div>

<!-- Accent card (primary top border) -->
<div class="card card-accent">
  <div class="card-header">Highlighted card</div>
  <p class="text-body">Featured or highlighted content.</p>
</div>
```

---

## 12. Alerts / Notes

```html
<div class="alert alert-info">
  <i class="ti ti-info-circle alert-icon"></i>
  <div>
    <div class="alert-title">Information</div>
    <div class="alert-body">Supporting description text.</div>
  </div>
</div>

<!-- Variants: alert-info | alert-success | alert-warning | alert-error -->
```

---

## 13. Notification Banner

```html
<div class="banner banner-info">
  <i class="ti ti-info-circle" style="font-size:18px;flex-shrink:0;margin-top:1px"></i>
  <div class="banner-content">
    <div class="banner-title">Heading text</div>
    <div class="banner-desc">Supporting description text.</div>
  </div>
  <button class="banner-close">&times;</button>
</div>

<!-- Variants: banner-info | banner-success | banner-warning | banner-error -->
```

---

## 14. Accordion

```html
<div class="accordion">
  <div class="accordion-item">
    <div class="accordion-trigger open" onclick="this.classList.toggle('open')">
      <span class="accordion-title">What is DRAD?</span>
      <i class="ti ti-chevron-up"></i>
    </div>
    <div class="accordion-body">Answer text goes here with full explanation.</div>
  </div>
  <div class="accordion-item">
    <div class="accordion-trigger" onclick="this.classList.toggle('open')">
      <span class="accordion-title">How do I raise a request?</span>
      <i class="ti ti-chevron-down"></i>
    </div>
    <!-- body hidden by default -->
  </div>
</div>
```

---

## 15. Tooltips

```html
<!-- Top tooltip -->
<div class="tooltip-wrap">
  <button class="btn btn-secondary btn-sm">Hover me</button>
  <div class="tooltip tooltip-dark tooltip-top">Tooltip message</div>
</div>

<!-- Bottom -->
<div class="tooltip-wrap">
  <button class="btn btn-secondary btn-sm">Hover me</button>
  <div class="tooltip tooltip-dark tooltip-bottom">Tooltip message</div>
</div>

<!-- Left -->
<div class="tooltip-wrap">
  <button class="btn btn-secondary btn-sm">Hover me</button>
  <div class="tooltip tooltip-dark tooltip-left">Tooltip message</div>
</div>

<!-- Right -->
<div class="tooltip-wrap">
  <button class="btn btn-secondary btn-sm">Hover me</button>
  <div class="tooltip tooltip-dark tooltip-right">Tooltip message</div>
</div>

<!-- Direction: tooltip-top | tooltip-bottom | tooltip-left | tooltip-right -->
<!-- Theme:     tooltip-dark | tooltip-light | tooltip-error | tooltip-warning | tooltip-success -->
```

---

## 16. Data Table

```html
<div class="table-wrap">
  <table class="dt">
    <thead>
      <tr>
        <th>Request ID</th>
        <th>Requested By</th>
        <th>Status</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="font-weight:700">D7389501</td>
        <td>A. Patel</td>
        <td><span class="badge badge-green">Approved</span></td>
      </tr>
    </tbody>
  </table>
</div>

<!-- Striped: add class dt-striped to <table> -->
```

---

## 17. Expanded Rows

```html
<div class="table-wrap">
  <table class="dt">
    <thead>
      <tr>
        <th style="width:32px"></th>
        <th>Request ID</th>
        <th>Status</th>
      </tr>
    </thead>
    <tbody>
      <!-- Trigger row -->
      <tr class="dt-expand-trigger" onclick="document.getElementById('exp1').style.display = document.getElementById('exp1').style.display==='none'?'table-row':'none'">
        <td><i class="ti ti-chevron-right" id="exp1-icon"></i></td>
        <td style="font-weight:700">D7389501</td>
        <td><span class="badge badge-green">Approved</span></td>
      </tr>
      <!-- Expanded row -->
      <tr id="exp1" style="display:none">
        <td colspan="3">
          <div class="dt-expand-body">
            <!-- Detail content here -->
            <strong>Approval history</strong>
            <p>L1: A. Sharma — Jan 11</p>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</div>
```

---

## 18. Stepper (Horizontal)

```html
<div class="stepper">
  <div class="stepper-step done">
    <div class="stepper-node"><i class="ti ti-check"></i></div>
    <div class="stepper-label">User Details</div>
  </div>
  <div class="stepper-step active">
    <div class="stepper-node">2</div>
    <div class="stepper-label">Schedule</div>
  </div>
  <div class="stepper-step">
    <div class="stepper-node">3</div>
    <div class="stepper-label">Review</div>
  </div>
  <div class="stepper-step">
    <div class="stepper-node">4</div>
    <div class="stepper-label">Submit</div>
  </div>
</div>

<!-- Step states: done | active | (default = pending) -->
```

---

## 19. Stepper (Vertical)

```html
<div class="stepper-v">
  <div class="stepper-v-step done">
    <div class="stepper-v-rail">
      <div class="stepper-v-node"><i class="ti ti-check"></i></div>
      <div class="stepper-v-line"></div>
    </div>
    <div class="stepper-v-content">
      <div class="stepper-v-title">User Details</div>
      <div class="stepper-v-sub">Completed</div>
    </div>
  </div>
  <div class="stepper-v-step active">
    <div class="stepper-v-rail">
      <div class="stepper-v-node">2</div>
      <div class="stepper-v-line"></div>
    </div>
    <div class="stepper-v-content">
      <div class="stepper-v-title">Schedule</div>
      <div class="stepper-v-sub">In progress</div>
    </div>
  </div>
</div>
```

---

## 20. Domino Tracker

```html
<div class="domino-track">
  <div class="domino-stage done">
    <div class="domino-node"><i class="ti ti-check" style="font-size:12px"></i></div>
    <div class="domino-stage-label">Request Raised</div>
    <div class="domino-stage-sub">Jan 10</div>
  </div>
  <div class="domino-stage done">
    <div class="domino-node"><i class="ti ti-check" style="font-size:12px"></i></div>
    <div class="domino-stage-label">L1 Approval</div>
    <div class="domino-stage-sub">Jan 11</div>
  </div>
  <div class="domino-stage active">
    <div class="domino-node"><i class="ti ti-loader" style="font-size:12px"></i></div>
    <div class="domino-stage-label">L2 Approval</div>
    <div class="domino-stage-sub">Pending</div>
  </div>
  <div class="domino-stage">
    <div class="domino-node">4</div>
    <div class="domino-stage-label">Delivery</div>
    <div class="domino-stage-sub">Waiting</div>
  </div>
</div>

<!-- Stage states: done | active | (default = pending) -->
```

---

## 21. Stat Strip

```html
<div class="stat-strip">
  <div class="stat-cell">
    <div class="stat-label">Records matched</div>
    <div class="stat-value primary">22,771</div>
  </div>
  <div class="stat-cell">
    <div class="stat-label">Quality score</div>
    <div class="stat-value success">98.5%</div>
  </div>
  <div class="stat-cell">
    <div class="stat-label">Processing time</div>
    <div class="stat-value">2.4 sec</div>
  </div>
  <div class="stat-cell">
    <div class="stat-label">Status</div>
    <div class="stat-value success">Ready</div>
  </div>
</div>
```

---

## 22. Summary Block

```html
<div class="summary">
  <div class="summary-header">Request details</div>
  <div class="summary-row">
    <span class="summary-key">Request ID</span>
    <span class="summary-val">D7389501</span>
  </div>
  <div class="summary-row">
    <span class="summary-key">Status</span>
    <span class="summary-val"><span class="badge badge-green">Approved</span></span>
  </div>
  <div class="summary-row">
    <span class="summary-key">Records</span>
    <span class="summary-val">22,771</span>
  </div>
</div>
```

---

## 23. Breadcrumb

```html
<nav class="breadcrumb">
  <a class="breadcrumb-item" href="#">Home</a>
  <span class="breadcrumb-sep">/</span>
  <a class="breadcrumb-item" href="#">Requests</a>
  <span class="breadcrumb-sep">/</span>
  <span class="breadcrumb-current">D7389501</span>
</nav>
```

---

## 24. Pagination

```html
<div class="pagination">
  <button class="page-btn" disabled>←</button>
  <button class="page-btn active">1</button>
  <button class="page-btn">2</button>
  <button class="page-btn">3</button>
  <button class="page-btn">...</button>
  <button class="page-btn">8</button>
  <button class="page-btn">→</button>
</div>
```

---

## 25. Modal

```html
<!-- Trigger button -->
<button class="btn btn-primary" onclick="document.getElementById('modal1').style.display='flex'">Open modal</button>

<!-- Modal (hidden by default) -->
<div class="modal-overlay" id="modal1" style="display:none" onclick="if(event.target===this)this.style.display='none'">
  <div class="modal">
    <div class="modal-header">
      <span class="modal-title">Confirm action</span>
      <button class="modal-close" onclick="document.getElementById('modal1').style.display='none'">&times;</button>
    </div>
    <div class="modal-body">
      Are you sure you want to submit this request? This will trigger the approval workflow.
    </div>
    <div class="modal-footer">
      <button class="btn btn-ghost btn-sm" onclick="document.getElementById('modal1').style.display='none'">Cancel</button>
      <button class="btn btn-primary btn-sm">Submit</button>
    </div>
  </div>
</div>
```

---

## 26. Success Screen

```html
<div class="success-screen">
  <div class="success-icon">
    <i class="ti ti-check" style="font-size:28px;color:var(--success)"></i>
  </div>
  <div class="success-title">Request submitted!</div>
  <div class="success-desc">
    Your request <span class="badge badge-blue">D7389501</span> has been received and is pending L1 approval.
  </div>
  <button class="btn btn-primary">View request status</button>
</div>
```

---

## 27. Utility Classes

| Class              | Effect                                  |
|--------------------|-----------------------------------------|
| `.flex`            | `display: flex`                         |
| `.flex-col`        | `flex-direction: column`                |
| `.items-center`    | `align-items: center`                   |
| `.justify-between` | `justify-content: space-between`        |
| `.gap-2/3/4/6`     | gap 8/12/16/24px                        |
| `.mt-2/4/6`        | margin-top 8/16/24px                    |
| `.mb-2/4`          | margin-bottom 8/16px                    |
| `.p-4/6`           | padding 16/24px                         |
| `.w-full`          | `width: 100%`                           |
| `.text-center`     | `text-align: center`                    |
| `.font-bold`       | `font-weight: 700`                      |
| `.font-medium`     | `font-weight: 500`                      |
| `.rounded`         | border-radius: var(--card-radius)       |
| `.border`          | 1px solid var(--border-light)           |
| `.sr-only`         | visually hidden, accessible to screen readers |

---

## 28. AI Prompt Templates

Use these exact prompts with any AI tool:

**Build a full page:**
> "Using the DRAD design system spec, build me a request detail page with: breadcrumb navigation, a stat strip with 4 KPIs, a summary block, a domino tracker with 5 stages, and a data table with expanded rows."

**Build a form:**
> "Using the DRAD design system spec, build me a 3-step form stepper for submitting a data suppression request. Step 1: requestor details (name, email, team). Step 2: schedule (date picker, frequency chips). Step 3: review summary block + submit button."

**Build a component:**
> "Using the DRAD design system spec, show me all 4 tooltip directions on a single page using the dark theme."

---

*End of DRAD Design System Spec v1.0*
