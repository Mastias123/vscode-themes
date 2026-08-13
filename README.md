# Cozy Forest Themes

This extension contains three dark VS Code themes inspired by warm amber light, deep forest greens, muted natural tones, and a high-contrast midnight spectrum. They are designed to keep the workbench calm while making code structure easy to scan.

## Included themes 

| Theme | Character | Best for |
| --- | --- | --- |
| **Cozy Forest** | Deep pine-green editor with restrained amber highlights | A cooler, quieter everyday coding environment |
| **Ember Canopy** | Rich ember and dark-brown surfaces with honey-gold accents | A warmer, more atmospheric version inspired by the reference artwork |
| **Midnight Spectrum** | Blue-charcoal editor with orange, green, blue, and rainbow symbol accents | A vibrant, high-contrast dark environment |

Cozy Forest and Ember Canopy use sage for types and properties, gold for functions, warm amber for active or focused elements, and muted teal for secondary contrast. Midnight Spectrum uses orange keywords, green strings and types, blue functions, and six-color bracket pairs.

## Develop locally

1. Open this folder in VS Code.
2. Press `F5` to open an **Extension Development Host** window.
3. In that new window, open the Command Palette with `Ctrl+Shift+P` (`Cmd+Shift+P` on macOS).
4. Run **Preferences: Color Theme** and choose **Cozy Forest**, **Ember Canopy**, or **Midnight Spectrum**.

Changes to the theme file are normally picked up after running **Developer: Reload Window** in the Extension Development Host.

## Install from this repository

Cloning this repository gives you the theme source. To install the themes in your normal VS Code instance, package that source into a VSIX file first:

```bash
git clone https://github.com/Mastias123/vscode-theme.git
cd vscode-theme
npx @vscode/vsce package
code --install-extension cozy-forest-theme-0.0.1.vsix
```

`npx` downloads and runs the VS Code extension packager without a global installation. The generated `.vsix` is the installable extension archive; its name changes when the `name` or `version` in `package.json` changes.

If the `code` command is unavailable, use **Extensions: Install from VSIX** from the Command Palette and choose the generated `.vsix` file. After installation, use **Preferences: Color Theme** to select a theme.

For a download that does not require packaging, maintainers can attach the generated `.vsix` file to a GitHub Release. Marketplace publishing is the option that makes the themes searchable and installable directly from VS Code's Extensions view.

## Update a local installation

A theme installed from a `.vsix` is a copy of the extension, so later changes in this repository do not appear in normal VS Code automatically. After changing or adding a theme:

1. Increase the `version` in `package.json` (for example, `0.0.1` to `0.0.2`).
2. Build a new package:

   ```bash
   npx @vscode/vsce package
   ```

3. Install the newly generated VSIX, using its new versioned filename:

   ```bash
   code --install-extension cozy-forest-theme-0.0.2.vsix
   ```

4. Run **Developer: Reload Window** if VS Code does not refresh the theme immediately.

Use the Extension Development Host workflow above for fast visual iteration; package and reinstall only when you want to update your normal VS Code installation.

## Repository layout

```text
.
├── package.json                     # Extension metadata and theme registration
├── themes/
│   ├── cozy-forest-theme.json       # The cooler pine-green theme
│   ├── ember-canopy-theme.json      # The warmer ember-brown theme
│   └── midnight-spectrum-theme.json # The blue-charcoal spectrum theme
└── README.md
```

## Editing the theme

The themes live in [`themes/cozy-forest-theme.json`](themes/cozy-forest-theme.json), [`themes/ember-canopy-theme.json`](themes/ember-canopy-theme.json), and [`themes/midnight-spectrum-theme.json`](themes/midnight-spectrum-theme.json). Keep their syntax roles aligned, while allowing their UI-surface colours to express each theme's character.

- `colors` controls the VS Code interface: editor, tabs, sidebar, terminal, lists, buttons, Git decorations, and diagnostics.
- `tokenColors` controls TextMate syntax scopes. It is the compatibility layer used by every language grammar.
- `semanticTokenColors` controls language-aware highlighting supplied by VS Code or a language server, such as classes, methods, parameters, and properties.

Keep general rules near the top of `tokenColors`, then group language-specific rules together. For example, HTML/JSX rules should sit together, followed by CSS/SCSS, JSON, and Markdown rules.

## Colour roles

Use colours by meaning instead of adding a new colour for every token:

| Role | Direction |
| --- | --- |
| Main surface | Cozy Forest: deep pine green; Ember Canopy: dark ember brown |
| Text | Warm parchment |
| Focus and keywords | Amber-orange |
| Types and properties | Sage green |
| Functions | Soft gold |
| Strings and numbers | Earthy gold / burnt orange |
| Information and links | Muted teal |
| Errors | Clay red |

Bright amber should be reserved for important, active, or focused UI so it keeps its impact. Ember Canopy deliberately uses more warm brown and orange in its surrounding workbench surfaces; Cozy Forest leaves more room for green.

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
node -e "for (const f of ['themes/cozy-forest-theme.json', 'themes/ember-canopy-theme.json', 'themes/midnight-spectrum-theme.json']) JSON.parse(require('fs').readFileSync(f)); console.log('Theme JSON is valid')"
```

Before publishing, test at least one file from each supported family: JavaScript/TypeScript, HTML/JSX, CSS/SCSS, JSON, Markdown, and a language with semantic highlighting such as Java or Python.

## Limits of a standard VS Code theme

A normal color theme can set solid UI and syntax colours, but it cannot package custom CSS, gradients, or a painted background image for the VS Code workbench. The intended native effect comes from layered solid surfaces, restrained amber highlights, and subtle translucent selections: pine-green in Cozy Forest and ember-brown in Ember Canopy.

## Publish later

When the theme is ready, update `version`, `publisher`, and the marketplace metadata in `package.json`, then package and publish it with the VS Code extension publishing tools.
