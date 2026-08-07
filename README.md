# Cozy Forest

Cozy Forest is a dark VS Code theme inspired by warm amber light, deep forest greens, and muted natural tones. It is designed to keep the workbench calm while making code structure easy to scan.

## Install locally

1. Open this folder in VS Code.
2. Press `F5` to open an **Extension Development Host** window.
3. In that new window, open the Command Palette with `Ctrl+Shift+P` (`Cmd+Shift+P` on macOS).
4. Run **Preferences: Color Theme** and choose **Cozy Forest**.

Changes to the theme file are normally picked up after running **Developer: Reload Window** in the Extension Development Host.

## Repository layout

```text
.
├── package.json                     # Extension metadata and theme registration
├── themes/
│   └── cozy-forest-theme.json       # All theme colours and syntax rules
└── README.md
```

## Editing the theme

The theme lives in [`themes/cozy-forest-theme.json`](themes/cozy-forest-theme.json).

- `colors` controls the VS Code interface: editor, tabs, sidebar, terminal, lists, buttons, Git decorations, and diagnostics.
- `tokenColors` controls TextMate syntax scopes. It is the compatibility layer used by every language grammar.
- `semanticTokenColors` controls language-aware highlighting supplied by VS Code or a language server, such as classes, methods, parameters, and properties.

Keep general rules near the top of `tokenColors`, then group language-specific rules together. For example, HTML/JSX rules should sit together, followed by CSS/SCSS, JSON, and Markdown rules.

## Colour roles

Use colours by meaning instead of adding a new colour for every token:

| Role | Direction in Cozy Forest |
| --- | --- |
| Main surface | Deep pine green / near-black |
| Text | Warm parchment |
| Focus and keywords | Amber-orange |
| Types and properties | Sage green |
| Functions | Soft gold |
| Strings and numbers | Earthy gold / burnt orange |
| Information and links | Muted teal |
| Errors | Clay red |

Bright amber should be reserved for important, active, or focused UI so it keeps its impact.

## Adding language support

1. Open a representative file for the language in the Extension Development Host.
2. Place the cursor on a token and run **Developer: Inspect Editor Tokens and Scopes**.
3. Copy the relevant TextMate scope into an existing or new `tokenColors` entry.
4. If the inspected token has a semantic token type, add a matching `semanticTokenColors` rule too.
5. Reload the window and compare the result in a real project.

Prefer precise scopes over broad ones. For example, use `variable.parameter` for parameters instead of a catch-all `identifier`, which can accidentally affect unrelated grammar tokens.

## Validate changes

The theme file must remain valid JSON. From the repository root:

```bash
node -e "JSON.parse(require('fs').readFileSync('themes/cozy-forest-theme.json')); console.log('Theme JSON is valid')"
```

Before publishing, test at least one file from each supported family: JavaScript/TypeScript, HTML/JSX, CSS/SCSS, JSON, Markdown, and a language with semantic highlighting such as Java or Python.

## Limits of a standard VS Code theme

A normal color theme can set solid UI and syntax colours, but it cannot package custom CSS, gradients, or a painted background image for the VS Code workbench. The intended native effect comes from layered dark green and brown surfaces, restrained amber highlights, and subtle translucent selections.

## Publish later

When the theme is ready, update `version`, `publisher`, and the marketplace metadata in `package.json`, then package and publish it with the VS Code extension publishing tools.
