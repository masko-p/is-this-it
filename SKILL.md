---
name: is-this-it
description: Render a lightweight HTML mockup from acceptance criteria, user stories, product notes, or feature requirements so a team can verify intended UI and flows before design or implementation.
---

# Is This It?

Render the requirement as written. Do not silently improve it.

## Workflow

1. Read the full source artifact, not just the acceptance criteria.
2. Extract user-visible requirements, explicit constraints, states, and out-of-scope notes.
3. Separate the UI-bearing and non-UI parts of each requirement. Keep the mapping visible in the output.
4. Group UI-bearing requirements into distinct surfaces or states such as list, detail, form, modal, empty state, validation state, or error state.
5. Build one self-contained HTML file from [assets/preview-template.html](assets/preview-template.html), keeping CSS and JS inline. Replace its placeholders, remove unused sections, and add the source-specific simulation and review notes. Do not require a build step or external assets unless the user explicitly asks for them.
6. Render only what the requirements justify. When the source is ambiguous or underspecified, make the smallest reasonable assumption and flag it instead of inventing detail.
7. Use realistic placeholder content so the screen is readable, but keep placeholders neutral and domain-appropriate.

## Output

- Preserve the template's header order: `Is This It?`, the source specification's title, `What you spec is what you get.`, then the local-simulation disclaimer.
- Keep the template's neutral styling independent of the project's visual language, design system, or graphic design specifications. The simulation is only for specification verification.
- Create one tab per surface for review navigation when multiple surfaces are required.
- Simulate explicitly described actions and their resulting state transitions locally without implementing backend services.
- Add visible requirement tags linked back to the full source criterion text in the review panel. Use stable criterion container ids and the template's `data-ac-return` links to scroll, focus, and briefly highlight the text without changing simulation state. Keep links outside labels and other interactive controls.
- Make rendered acceptance criteria in the review panel clickable: reveal the matching surface or local demo state, scroll to the implementing element, focus it, and briefly highlight it. Use the template's `data-ac-link` navigation and state-reveal hook. Explain when navigation changes the simulated state, provide separate links for distinct outcomes, and leave non-UI criteria marked as unverified without fabricated targets.
- Include a review panel that lists:
  - rendered requirements and where they appear
  - non-UI parts marked as not rendered and not verified by the preview
  - ambiguities, gaps, or assumptions

## Delivery

- Save the mockup at the path requested by the user.
- If no path is given, save next to the source file as `<source-stem>-preview.html`; for example, `checkout.md` becomes `checkout-preview.html`.
- If the source has no local file, save `<short-topic>-preview.html` in the working directory unless the user specified a path.
- Immediately after saving, open the file in the system default browser using a platform-appropriate launcher such as `open`, `xdg-open`, or `start`.
- Tell the reviewer to compare the mockup against the intended behavior. Check mismatches against the source: correct rendering errors and flag ambiguous or missing requirements for clarification.
