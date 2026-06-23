# Contributing

Contributions are welcome. Please read this guide before opening a pull request.

## What belongs in this list

This registry is for resources that help operators, architects, procurement teams, and coding agents understand and achieve compliance with NVIDIA software and GPU licensing. Acceptable entries include:

- Official NVIDIA license agreements, EULAs, and product-specific licensing guides.
- Official NVIDIA portals, support resources, and documentation for NVAIE, vGPU, NIM, NGC, and NLS.
- Tools that automate license discovery, SBOM generation, or compliance checks for NVIDIA software.
- Community-run calculators, checklists, or reference implementations that aid compliance.

## What does **not** belong

- General NVIDIA product documentation that does not address licensing or compliance.
- Unofficial legal interpretations presented as definitive advice.
- Closed-source or paywalled-only tools with no public documentation.
- Duplicate entries.

## Quality bar

Every submission must be:

1. **Publicly accessible** — open source or publicly documented.
2. **Current or maintained** — links should resolve to current documentation; prefer official sources.
3. **Documented** — a real README or page with setup/usage instructions.
4. **Correctly categorized** — placed under the licensing topic it primarily targets.
5. **Honestly labeled** — use the `Official` or `Community` badge.

## Entry format

Use this pattern:

```markdown
- **[Name](URL)** `Official` — One-sentence description.
  - Install: `command here`
```

If there is no install command, omit the install line.

## Sections

The README is organized by **licensing topic**, not by resource type. New sections are allowed only if they contain at least three entries.

## Pull request process

1. Fork the repository.
2. Add your entry in the correct section.
3. Run `./scripts/validate-links.sh` and fix any broken links or anchors.
4. Open a pull request with a clear description of the resource and why it fits.

One resource per pull request is preferred.
