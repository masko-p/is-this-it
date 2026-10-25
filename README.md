# Is This It?

*What you spec is what you get.*

Turn written requirements into a self-contained HTML preview so your team can see what the words describe before design or implementation.

## Installation

Install the skill as a directory named `is-this-it`, with its template included.

1. Download or clone this repository.
2. Find the skills directory configured for your tool. Its location and whether it applies to one project or all projects depend on the tool; there is no universal installation path.
3. Copy the repository contents into `is-this-it/` inside that directory. Put `SKILL.md` directly at the installed skill's root and preserve the `assets/` subdirectory.
4. Enable or reload skills using your tool's normal mechanism, if required.

Minimum required layout:

```text
<skills-directory>/is-this-it/
|-- SKILL.md
`-- assets/
    `-- preview-template.html
```

`<skills-directory>` is a placeholder for the actual configured directory. The repository checkout may have any name; the installed skill directory is `is-this-it`.

Both [SKILL.md](SKILL.md) and [assets/preview-template.html](assets/preview-template.html) are required for generation. `README.md` and `example/` are optional documentation and examples.

The agent must be able to read both required files and the source requirements, write the generated HTML, and launch a local browser to open it automatically. The finished preview only needs a browser: it has no dependency on the installed skill directory and requires no build step.

## Manual Use

If your tool does not discover skill directories, make the complete skill directory accessible to the agent and give it the actual path to `SKILL.md`. If using file attachments instead, supply both `SKILL.md` and `preview-template.html`, identifying the latter as the file referenced by `assets/preview-template.html`.

For agents: read `SKILL.md` as the workflow entry point. Resolve its relative resource paths from the directory containing `SKILL.md`, not from the current working directory. Read the HTML template as a starting asset and generate a separate preview; keep the installed template unchanged. Loading only `SKILL.md` is incomplete.

## Use

Once the skill is installed or both required files are available, ask in your own words:

> Is this it for promo codes at checkout? Let me try it and see if it's what we had in mind.

For an explicit invocation, use a slash command if your tool supports it:

```text
/is-this-it how we want promo codes to work at checkout?
```

Name the feature or describe the behavior you want to review. The agent should find the relevant specification in the project or conversation; if it cannot identify the source, it should ask for the missing context.

Use it to align expectations about screens and behavior, walk through acceptance criteria, or expose ambiguities before implementation.

## Output

By default, the preview is saved next to the source file using its filename without the final extension, followed by `-preview.html`:

```text
checkout.md -> checkout-preview.html
```

For requirements without a local source file, it uses `<short-topic>-preview.html` in the working directory. An explicitly requested output path takes precedence. The saved preview opens immediately in the system default browser.

- One HTML file with inline styles and scripts. By default, viewing it requires no external assets or installed skill files.
- Screens and states justified by the requirements, with local simulation of explicitly described actions.
- Visible labels connecting rendered elements to their requirements.
- Clickable acceptance criteria that reveal the matching state, move focus to the linked element, and briefly highlight it.
- A review panel showing coverage, assumptions, ambiguities, and non-UI behavior that the preview cannot verify.

## Preview Template

Every preview starts from the [shared HTML template](assets/preview-template.html): Is This It? branding, the source specification's title, the slogan, and a local-simulation disclaimer above the simulation and review panel.

The template uses neutral styling. It does not account for the project's visual language, design system, or graphic design specifications. The simulation is only for specification verification.

## Example

See the [promo-code checkout specification](example/checkout.md) and its [interactive HTML preview](example/checkout-preview.html).

Open `example/checkout-preview.html` locally. Select a validation outcome in the review controls, apply a code, and place an order to inspect the confirmation. Apply the same code twice to check duplicate handling, or choose a service failure to try the recovery flow. All actions are simulated locally.

Click an acceptance criterion in the coverage panel to show its local demo state and focus the matching element. AC3 provides separate expired and invalid outcomes; AC6 links to both checkout and confirmation. Scenario links may change the current simulation. Non-UI criteria remain labeled as unverified.

## Review

Compare the preview with the behavior you intended. Check differences against the source: fix rendering errors and clarify ambiguous or missing requirements.

The preview is an artifact for reviewing intent. It does not establish a final design or verify backend behavior.
