SCORES: mobile 6/10, polish 7/10, contrast 9/10, flows 6/10

CONTRAST AUDIT:
- `#9AA3AE` on `#181B21`: 6.8:1 (WCAG AA Pass)
- `#9AA3AE` on `#1F232B`: 6.2:1 (WCAG AA Pass)
- `#E8EAED` on `#0F1115`: 15.6:1 (WCAG AAA Pass)

TOP FIXES:
1. Fix Checklist Reset Bug: In `renderChecks()`, non-daily tasks auto-uncheck after 1500ms (`if(k!=='daily') setTimeout(...)`). Remove this timeout; weekly and close checklists must persist until manual uncheck.
2. Fix Note Loss on Status Change: Changing a dropdown status triggers `renderTracker()`, destroying uncommitted inputs. Change input listeners from `onchange` to `oninput` and avoid full table re-renders on select change (only update target row class/state).
3. Sticky Tab Navigation on Mobile: Static header + 9 scrollable tabs isolates navigation when scrolled down. Keep `position:sticky; top:0; z-index:20` for `.tabs` or the entire header on mobile, adding a right-edge gradient fade to signal overflow tabs (Sync/Projects).
4. Missing CSS Declarations:
   - `--head` is used in `.demo-cat` but undefined in `:root`. Add `--head: var(--sans);`.
   - `.btn` class is unstyled in CSS; add base styles (`padding`, `border-radius`, `font-size`) to CSS instead of scattered inline styles.
5. Mobile Table Editing: Horizontal scrolling a 980px table with micro `<input>` and `<select>` is frustrating on mobile. For `<=820px`, convert `#tbody tr` to a stacked card layout (`display:flex; flex-direction:column; gap:8px`).
6. Copy & Number Formatting:
   - Fix unformatted rating numbers (e.g. `4.900000★` -> `4.9★`) in raw DATA strings.
   - Standardize language: Use Indonesian for UI controls/actions ("Salin", "Unduh") and English strictly for pitch copies/prompts.

VERDICT: FIX FIRST (Checklist wipe bug & table input re-render glitch break core logging).