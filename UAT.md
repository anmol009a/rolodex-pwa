# Rolodex PWA — UAT Results

> **Status**: Testing Complete  
> **Date**: 2026-06-25  
> **Tester**: Anmol

---

## Summary Scorecard

| Area | Total | ✅ Pass | ⚠️ Partial | ❌ Fail | ⏭ Skip |
|------|-------|---------|-----------|--------|--------|
| A — Adding | 6 | 3 | 1 | 2 | 0 |
| B — Editing | 5 | 4 | 1 | 0 | 0 |
| C — Deleting | 5 | 5 | 0 | 0 | 0 |
| D — Tagging | 6 | 6 | 0 | 0 | 0 |
| E — Search | 9 | 8 | 0 | 1 | 0 |
| F — Filters | 6 | 0 | 0 | 6 | 0 |
| G — Duplicates/Sort | 3 | 2 | 0 | 1 | 0 |
| H — Modal/UX | 5 | 5 | 0 | 0 | 0 |
| I — Export/Import | 10 | 9 | 0 | 1 | 0 |
| J — Nudge Banner | 6 | 0 | 0 | 0 | 6 |
| K — Persistence | 4 | 3 | 0 | 1 | 0 |
| L — Edge Cases | 6 | 6 | 0 | 0 | 0 |
| **TOTAL** | **71** | **51** | **2** | **11** | **6** |

---

## Area 1 — Adding a Person

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| A1 | Add person with valid name | ⚠️ Partial | Card appears correctly. However "✓ saved" flash appears at the **bottom of the card**, which is not visible during normal use. Flash also disappears — no persistent saved state. **Request: Google Docs-style save indicator near the name field, persistent.** |
| A2 | Add person with NO name | ❌ Fail | Unnamed card IS created and shows as "(unnamed)" in the grid. **Should be blocked — a person without a name should not be saveable.** |
| A3 | Add person — all fields filled | ✅ Pass | All data persists correctly. |
| A4 | Counter pill updates | ✅ Pass | Pill updates immediately. |
| A5 | Auto-save fires after typing | ❌ Fail | Same issue as A1 — "✓ saved" not visible. No persistent indicator. |
| A6 | First person — empty state disappears | ✅ Pass | Empty state hides correctly. |

---

## Area 2 — Editing a Person

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| B1 | Edit name | ✅ Pass | |
| B2 | Edit phone | ✅ Pass | |
| B3 | Edit birthday | ⚠️ Partial | Functional, but **future dates can be selected** — this should not be allowed. |
| B4 | Clear a field | ✅ Pass | |
| B5 | Birthday display format | ✅ Pass | Shows as "Month Day" (e.g. "Jun 25"). |

---

## Area 3 — Deleting a Person

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| C1 | Delete with confirm | ✅ Pass | |
| C2 | Cancel delete | ✅ Pass | |
| C3 | Delete last person | ✅ Pass | |
| C4 | Delete named person confirm text | ✅ Pass | |
| C5 | Delete unnamed person confirm text | ✅ Pass | |

---

## Area 4 — Tagging

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| D1 | Default tag is "Other" | ✅ Pass | |
| D2 | All 5 tags available | ✅ Pass | |
| D3 | Tag selection changes color | ✅ Pass | |
| D4 | Tag shown on grid card | ✅ Pass | |
| D5 | Tag persists after reload | ✅ Pass | |
| D6 | Only one tag selectable | ✅ Pass | |

---

## Area 5 — Search

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| E1 | Search by name | ✅ Pass | |
| E2 | Search by work | ✅ Pass | |
| E3 | Search by notes | ✅ Pass | |
| E4 | Search by phone | ✅ Pass | |
| E5 | Search by likes | ✅ Pass | |
| E6 | Case-insensitive search | ✅ Pass | |
| E7 | No matches state | ✅ Pass | |
| E8 | Clear search restores grid | ✅ Pass | |
| E9 | Search + filter combined | ❌ Fail | **Filter chips are not visible/functional** — there is only a search bar, no tag filter chips in the UI. |

---

## Area 6 — Filter Chips

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| F1 | "All" filter selected by default | ❌ Fail | **Filter chips do not appear in the UI at all.** |
| F2 | Filter by tag | ❌ Fail | No filter chips present. |
| F3 | Filter count doesn't change pill | ❌ Fail | Cannot test — no filters. |
| F4 | Filter chip active styling | ❌ Fail | Cannot test — no filters. |
| F5 | Switch filter | ❌ Fail | Cannot test — no filters. |
| F6 | Back to All | ❌ Fail | Cannot test — no filters. |

> [!CAUTION]
> **Root cause to investigate**: The code has `renderFilters()` and `#filterRow` in the HTML, but chips are not appearing. Possible JS error silently suppressing render, or a CSS issue hiding the row.

---

## Area 7 — Duplicate / Name Handling

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| G1 | Duplicate name allowed | ❌ Fail | **Two people with the same name can be added.** This is not desired behavior — duplicates should be prevented at add-time. |
| G2 | Sort is alphabetical | ✅ Pass | |
| G3 | Unnamed cards sort | ✅ Pass | "(unnamed)" appears first in the grid — but **unnamed people should not be creatable at all** (linked to A2). |

---

## Area 8 — Modal / UX Behaviour

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| H1 | Close via ✕ button | ✅ Pass | |
| H2 | Close via overlay click | ✅ Pass | |
| H3 | Close via Escape key | ✅ Pass | |
| H4 | Name field auto-focused | ✅ Pass | |
| H5 | Modal scrollable | ✅ Pass | |

---

## Area 9 — Export / Import / Backup

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| I1 | Backup menu toggle | ✅ Pass | |
| I2 | Backup menu closes on outside click | ✅ Pass | |
| I3 | Export to file | ✅ Pass | |
| I4 | Export file structure | ✅ Pass | |
| I5 | Backup status updates after export | ✅ Pass | |
| I6 | Import — Merge mode | ✅ Pass | |
| I7 | Import — Replace mode | ✅ Pass | |
| I8 | Import invalid file | ✅ Pass | |
| I9 | Merge skips duplicates | ✅ Pass | |
| I10 | Save to Drive (desktop) | ❌ Fail | Shows popup at bottom of screen saying to use Export instead, rather than silently falling back to a download. Minor UX note — functionally works, but messaging could be improved. |

---

## Area 10 — Backup Nudge Banner

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| J1–J6 | All nudge banner tests | ⏭ Skipped | Skipped by tester. |

---

## Area 11 — Persistence (localStorage)

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| K1 | Data survives page reload | ✅ Pass | |
| K2 | Data survives browser restart | ✅ Pass | |
| K3 | Filter state NOT persisted | ❌ Fail | No filter chips present — cannot test. Linked to F1–F6. |
| K4 | Backup meta persists | ✅ Pass | |

---

## Area 12 — Edge Cases & Robustness

| # | Test Case | Result | Finding |
|---|-----------|--------|---------|
| L1 | HTML in name field | ✅ Pass | XSS safely escaped. |
| L2 | Very long name | ✅ Pass | Text clips/truncates correctly. |
| L3 | Emoji in fields | ✅ Pass | |
| L4 | Special characters | ✅ Pass | |
| L5 | Birthday invalid input | ✅ Pass | |
| L6 | 100+ people performance | ✅ Pass | Tested with 150-person import — no visible lag. |

---

## Bug List (Prioritised)

| # | Bug | Severity | Area |
|---|-----|----------|------|
| BUG-01 | Filter chips not rendering in UI | 🔴 High | F1-F6, E9, K3 |
| BUG-02 | Person with no name can be created and saved | 🔴 High | A2, G3 |
| BUG-03 | Duplicate names can be added without warning | 🟠 Medium | G1 |
| BUG-04 | "✓ saved" flash is invisible (bottom of card, off-screen) | 🟠 Medium | A1, A5 |
| BUG-05 | Birthday field allows future dates | 🟡 Low | B3 |
| BUG-06 | "Save to Drive" on desktop shows awkward fallback message | 🟡 Low | I10 |

---

## Enhancement Requests

| # | Enhancement | Notes |
|---|-------------|-------|
| ENH-01 | Persistent Google Docs-style save indicator near name field | Replace transient "✓ saved" with a always-visible "Saved" / "Saving…" status near the card header |

---

## Decisions & Fix Backlog

> **Status**: Documented. Not yet implemented. Fix in a future session.

| Bug | Decision | Implementation Notes |
|-----|----------|----------------------|
| BUG-01 — Filter chips missing | **Fix** | Debug `renderFilters()` — investigate why `#filterRow` is not rendering chips. Likely a silent JS error or CSS issue. |
| BUG-02 — Nameless person can be saved | **Fix — Block (discard)** | On `closeCard()`, if `fName.value.trim()` is empty, delete the person from the array and persist. Show toast: *"Name is required — person discarded."* |
| BUG-03 — Duplicate names allowed | **Fix — Block with visual feedback** | In `doSave()`, check if any other person (different `id`) shares the same name (case-insensitive). If duplicate found: apply red border to name field + show inline error message. Prevent saving until name is changed. |
| BUG-04 / ENH-01 — Save indicator invisible | **Fix — Google Docs style** | Remove bottom "✓ saved" flash. Add an always-visible **"Saved ✓" / "Saving…"** status text inline near the name field inside the modal. |
| BUG-05 — Future birthday selectable | **Fix** | Set `max` attribute on `#fBirthday` to today's date (`new Date().toISOString().slice(0,10)`) on page init. |
| BUG-06 — Save to Drive desktop message | **Won't Fix — By Design** | Desktop fallback to file download is intentional. Toast message is acceptable. |
