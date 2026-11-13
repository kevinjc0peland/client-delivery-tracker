# Client Delivery Tracker

A single-user, browser-local prototype for Kevin Copeland LLC's consulting delivery workflow. This app is separate from CreditLuna.

## Included workflow

- Client onboarding: contact details, offer, start date, journey stage, and onboarding checklist.
- Session notes: focus, observations, commitments, and next step.
- Follow-ups: owner, due date, status, and next action.
- Payment handoffs: amount, due date, status, and administrative handoff.
- Testimonials: request date, permission status, quote, and readiness.
- Overview: active clients, open follow-ups, payment attention items, and recent activity.
- Backup: export/import the full local dataset as JSON.

## Run it

Keep index.html, styles.css, and app.js together and open index.html in a modern browser. No build step or external dependency. An optional local server: python3 -m http.server 8000, then open http://localhost:8000/ in the folder served. The separate preview.html has CSS and JS inlined.

## Changelog — 2026-11-12

1. Import safety: validate all five arrays and every record before mutation; check strings, IDs, duplicate IDs, real dates, enums, onboarding checklists and nonnegative amounts. Unexpected fields and malformed files are rejected as a whole. Missing optional text/date fields normalize to empty strings. Require confirmation that import REPLACES ALL current data. Start a dated safety JSON download before committing; failed persistence keeps the existing live data. Input files are capped at 20 MB and arrays at 50,000 records. Browsers control final download completion; confirm the safety file reached Downloads.
2. Reset: fresh-array factory replaces shared blank-data arrays in initialization and clear paths.
3. Escaping: escape dynamic IDs, attribute/input values and invalid-date fallback text. Imported records are rendered only after schema validation.
4. Storage: catch read/write failures; show a persistent visible warning. Do not show a saved-success toast after a failed write. Clear and import commit live state only after persistence succeeds.
5. Mobile: keep export, import and clear visible in a wrapping backup bar, with 44px-minimum touch targets. Import remains keyboard-focusable.
6. Dates: use browser-local calendar components for defaults and dated backup filenames (including a local time suffix).
7. Events: stable-container event delegation binds once; searches and renders do not accumulate listeners.
8. Branding: Kevin Copeland LLC navy #1B2A4A, Carolina blue #4B9CD3, off-white #F7F4EC, pale blue #E5EFF4; updated theme-color and blue accents. Retain Inter and system fallbacks. Green/amber/red remain semantic status colors.

## Known limitations still open

- Session editing is not implemented (add/delete only).
- Deleting a client does not clean up orphaned related records; they display as Unassigned client.
- Testimonial permission/readiness is manually recorded; no new consent workflow or enforcement was added.
- Single-user localStorage key: clientDeliveryTracker.v1. No encryption, authentication, sync, role-based access, or secure client portal. Exports are plain JSON. Use placeholder/test data, not sensitive client details. Production needs a secure authenticated backend, encryption, access controls, audit logs and privacy processes.
- Standard edits remain in memory if storage fails; heed the persistent NOT SAVED warning and export before leaving. Download initiation cannot guarantee a browser saved the file; check Downloads, especially on iPhone.

## Preview

Temporary public preview hosted for 7 days; anyone with its link can open it. Use test data only. Its local records are separate from a local-file installation and do not transfer automatically. No Google Drive file was modified or uploaded.

## Round two changelog — 2026-11-12

- Locked KCLLC typography: Arial/Helvetica for body, labels, buttons, tables and kickers; Georgia for app/brand and main editorial section headings. Uppercase kicker letter spacing is unchanged. This supersedes round one's Inter stack.
- Strengthened the only changed muted-text color: --muted #52677B → #40566C. On white, contrast improves 5.858:1 → 7.593:1; off-white #F7F4EC, 5.330:1 → 6.908:1; pale blue #E5EFF4, 5.017:1 → 6.503:1. On Carolina blue surfaces use navy #1B2A4A (4.737:1), not the muted token. On navy surfaces retain pale blue #E5EFF4 (12.179:1). No universal foreground color works on both light and dark surfaces; foregrounds are paired with their actual backgrounds.
- First use: with zero clients, show a friendly Add client guide and working button. It disappears once a client exists and returns after Clear.
- Mobile navigation: all six sections are visible in a two-column grid with 44px-minimum targets, instead of a narrow horizontal tab strip.
- Clients remain cards, not a table. Cards wrap long text. Tables have a labelled keyboard-focusable horizontal-scroll region; at phone widths the table has a 660px minimum and wrapped cells, containing scroll without widening the page. Search/add toolbars wrap.
- Preview-only visible note: Temporary preview - test data only. It is omitted from the permanent-deploy index.html download.
- All eight round-one safety fixes and the same localStorage key remain in place. The existing session-editing, orphan-cleanup and testimonial-consent limitations are unchanged.

## Optional client details — November 12, 2026

- Client add/edit forms support optional email, multi-line physical mailing address and birthday. Email is displayed as a mailto link, addresses preserve line breaks, and birthdays use the existing local-date formatter. Missing values on older records are safe.
- Email and address import as optional strings (20,000-character limit, no strict email format); birthday is empty or a real YYYY-MM-DD date. Missing fields normalize to empty strings. All other strict import checks remain unchanged.
- Contact details persist locally and are included in JSON exports/imports. Form labels retain Arial uppercase styling and letter spacing, inputs have 44px minimum targets, and client details wrap on phone-width cards. These personal details remain unencrypted browser-local data; avoid sensitive information and protect exported backups.

## Optional last name — November 12, 2026

- Added an optional Last name input immediately after the unchanged Name field in client add/edit forms. Client card headings append it with a space when present and render exactly as before when absent; values remain escaped.
- Client search now matches last names as well as existing name, offer and email fields.
- Last name follows the existing optional-string import rules (up to 20,000 characters); older backups without it still import, and JSON exports/imports preserve it. Other validation strictness is unchanged. The field reuses the existing Arial uppercase label styling and 44px minimum input target.
