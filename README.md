# OJ-branding-preset

Shared brand color tokens — one source of truth for every project (MERN, Laravel, etc).

## Folder structure

```
OJ-branding-preset/
├── index.js             ← package entry point, exports tokens/tokens.json as JS
├── css/
│   ├── theme.css        ← color tokens (light + dark)
│   └── scrollbar.css    ← optional hidden-scrollbar rules
├── scripts/             ← reserved for future build/gen scripts (empty for now)
├── tokens/
│   └── tokens.json      ← color values as plain JSON (source of truth)
├── ui/
│   └── CustomScrollbar.tsx  ← optional React scrollbar component
├── package.json
└── README.md
```

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

Then proceed to installing the package below.

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

## Usage — Tailwind v4 / shadcn projects (CSS)

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

## Optional — hide native scrollbars

If a project wants the scrollbar-hidden look too, import it separately:

```css
@import "oj-branding-preset/css/theme.css";
@import "oj-branding-preset/css/scrollbar.css";
```

Leave it out for projects where you want the native scrollbar to show.

## Optional — custom drag-to-scroll bar (React)

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

## Usage — JS / Node (e.g. Laravel Mix, Vite config, scripts)

```js
const tokens = require('oj-branding-preset');

console.log(tokens.light.primary); // "#1b5def"
console.log(tokens.dark.background); // "#0f1117"
```

## Usage — Laravel Blade / PHP

Read the JSON directly:

```php
$tokens = json_decode(file_get_contents(
    base_path('node_modules/oj-branding-preset/tokens/tokens.json')
), true);

$primary = $tokens['light']['primary']; // #1b5def
```

## Full walkthrough (new project, step by step)

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
the install worked and you're ready to import it in your code (see usage sections below).

If `npm install` is run in a folder with no `package.json`, it will either fail
or install into the wrong place — always run `npm init -y` first for any new folder.

## Updating tokens

1. Edit `theme.css` AND `tokens.json` together (keep them in sync).
2. Bump the version in `package.json`.
3. Commit, tag (`git tag v1.0.1 && git push --tags`), push.
4. In consumer projects: `npm update oj-branding-preset`.