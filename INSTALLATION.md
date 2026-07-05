# Installation

## Prerequisites

Before installing, the target project folder **must already be an npm project**
(i.e. have its own `package.json`). `npm install` needs somewhere to register
the dependency — without a `package.json`, the install has nothing to attach to.

Check if your project already has one:
```bash
dir package.json        # Windows PowerShell
ls package.json          # Mac/Linux
```

If it doesn't exist yet, create it first:
```bash
npm init -y
```

## Install

```bash
npm install github:Wenoxxxx/OJ-branding-preset
```

Pin to a tag once stable:
```bash
npm install github:Wenoxxxx/OJ-branding-preset#v1.0.0
```

## Verify the install

```bash
dir node_modules\oj-branding-preset        # Windows
ls node_modules/oj-branding-preset          # Mac/Linux
```

You should see: `css/`, `scripts/`, `tokens/`, `ui/`, `index.js`, `package.json`.

## Full walkthrough (brand new project, step by step)

This covers the exact scenario where a project folder is brand new and hasn't
run any npm commands yet.

```bash
# 1. Go into your project folder
cd my-project

# 2. Check if package.json already exists
dir package.json          # Windows
ls package.json            # Mac/Linux

# 3. If it doesn't exist, initialize npm first — this is required
npm init -y

# 4. Now install the branding preset
npm install github:Wenoxxxx/OJ-branding-preset

# 5. Confirm it installed correctly
dir node_modules\oj-branding-preset       # Windows
ls node_modules/oj-branding-preset         # Mac/Linux
```

If step 5 shows `css/`, `scripts/`, `tokens/`, `ui/`, `index.js`, `package.json` —
the install worked and you're ready to import it in your code (see below).

If `npm install` is run in a folder with no `package.json`, it will either fail
or install into the wrong place — always run `npm init -y` first for any new folder.

---

## Usage — Tailwind v4 / shadcn projects (MERN / React)

In your project's `globals.css`, import the token file *before* your `@theme inline` block:

```css
@import "tailwindcss";
@import "oj-branding-preset/css/theme.css";

@theme inline {
  --color-primary: var(--primary);
  --color-background: var(--background);
  /* ...map the rest as needed */
}
```

Keep app-specific overrides (fonts, forced border-radius, etc.) in your own `globals.css`
— don't put them in this package.

### Optional — hide native scrollbars

```css
@import "oj-branding-preset/css/theme.css";
@import "oj-branding-preset/css/scrollbar.css";
```

Leave it out for projects where you want the native scrollbar to show.

### Optional — custom drag-to-scroll bar (React)

A styled scrollbar component that tracks a `[data-slot="sidebar-inset"]` scroll pane
(shadcn `SidebarInset`) and draws a thin brand-blue thumb instead of the native bar.

```tsx
import { CustomScrollbar } from "oj-branding-preset/ui/CustomScrollbar"

// render once, near the root of your layout
<CustomScrollbar />
```

Requires `react` (>=18) in the consuming project — it's a peer dependency, not bundled.
Ships as raw `.tsx`; your bundler (Vite/Next) compiles it like any other component.

Note: the drag-thumb glow is hardcoded to `rgba(27,93,239,0.4)` (brand blue at 40% alpha).
If the brand primary color ever changes, update that value in `ui/CustomScrollbar.tsx`
too — it isn't pulled from `theme.css` automatically.

---

## Usage — Brand fonts (Poppins, JetBrains Mono)

Import the font-face file once, then reference the family names normally in your CSS:

```css
@import "oj-branding-preset/assets/fonts/fonts.css";

body {
  font-family: 'Poppins', sans-serif;
}

code, pre {
  font-family: 'JetBrains Mono', monospace;
}
```

⚠️ Verify the actual filenames inside `assets/fonts/Poppins/` and
`assets/fonts/JetBrains Mono/` match what's referenced in `fonts.css` — the
`@font-face` `src` paths must exactly match the real file names (case-sensitive),
or the fonts silently fail to load.

## Usage — Logos

Reference the file directly wherever your bundler/framework supports importing
static assets from `node_modules`:

```tsx
import logo from "oj-branding-preset/assets/logos/logo.svg"

<img src={logo} alt="Logo" />
```

Or in plain HTML/CSS:
```css
.logo {
  background-image: url("oj-branding-preset/assets/logos/logo.svg");
}
```

Adjust the filename to match whatever you actually named the file(s) in
`assets/logos/`.

---

## Usage — plain JS / Node (e.g. Vite config, build scripts)

```js
const tokens = require('oj-branding-preset');

console.log(tokens.light.primary); // "#1b5def"
console.log(tokens.dark.background); // "#0f1117"
```

---

## Usage — Laravel Blade / PHP

Read the JSON directly:

```php
$tokens = json_decode(file_get_contents(
    base_path('node_modules/oj-branding-preset/tokens/tokens.json')
), true);

$primary = $tokens['light']['primary']; // #1b5def
```