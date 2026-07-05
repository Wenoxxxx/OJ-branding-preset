# OJ-branding-preset

Shared brand color tokens — one source of truth for every project (MERN, Laravel, etc).

## Folder structure

```
OJ-branding-preset/
├── css/
│   ├── theme.css       ← color tokens (light + dark)
│   └── scrollbar.css   ← optional hidden-scrollbar rules
├── scripts/
│   └── index.js        ← exports tokens/tokens.json as a JS object
├── tokens/
│   └── tokens.json      ← color values as plain JSON (source of truth)
├── ui/
│   └── CustomScrollbar.tsx  ← optional React scrollbar component
├── package.json
└── README.md
```

## Install

```bash
npm install github:yourname/OJ-branding-preset
```

Pin to a tag once stable:
```bash
npm install github:yourname/OJ-branding-preset#v1.0.0
```

## Usage — Tailwind v4 / shadcn projects (CSS)

In your project's `globals.css`, import the token file *before* your `@theme inline` block:

```css
@import "tailwindcss";
@import "oj-branding-preset/theme.css";

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
@import "oj-branding-preset/theme.css";
@import "oj-branding-preset/scrollbar.css";
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

## Updating tokens

1. Edit `theme.css` AND `tokens.json` together (keep them in sync).
2. Bump the version in `package.json`.
3. Commit, tag (`git tag v1.0.1 && git push --tags`), push.
4. In consumer projects: `npm update oj-branding-preset`.
