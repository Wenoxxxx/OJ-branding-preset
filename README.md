# OJ-branding-preset

Shared brand color tokens — one source of truth for every project (MERN, Laravel, etc).

## What's inside

- **Color tokens** (light + dark) as CSS variables and plain JSON
- **Brand fonts** (Poppins, JetBrains Mono) with ready-made `@font-face` CSS
- **Logo assets** (.svg/.png)
- **Optional** hidden-scrollbar CSS
- **Optional** custom drag-to-scroll React component

## Folder structure

```
OJ-branding-preset/
├── index.js             ← package entry point, exports tokens/tokens.json as JS
├── css/
│   ├── theme.css        ← color tokens (light + dark)
│   └── scrollbar.css    ← optional hidden-scrollbar rules
├── assets/
│   ├── fonts/
│   │   ├── fonts.css    ← @font-face declarations for both families
│   │   ├── Poppins/
│   │   └── JetBrains Mono/
│   └── logos/           ← logo image files (.svg/.png)
├── scripts/             ← reserved for future build/gen scripts (empty for now)
├── tokens/
│   └── tokens.json      ← color values as plain JSON (source of truth)
├── ui/
│   └── CustomScrollbar.tsx  ← optional React scrollbar component
├── package.json
├── README.md
├── INSTALLATION.md       ← full setup + usage per platform (MERN, Laravel, plain JS)
└── UPDATING.md           ← how to push changes and refresh installs elsewhere
```

## Adding or removing files

Any file inside `css/`, `tokens/`, `ui/`, `assets/`, or `scripts/` is automatically
importable — `package.json` uses wildcard exports for these folders, so adding,
renaming, or removing a file inside them doesn't require touching `package.json`.

```tsx
// works automatically, no exports edit needed
import newLogo from "oj-branding-preset/assets/logos/logo-dark.svg"
```

A manual edit is only needed if you create a **brand-new top-level folder**
(something other than the five above) — that one new folder needs one line
added to both `files` and `exports` in `package.json`.

## Quick install

```bash
npm install github:Wenoxxxx/OJ-branding-preset
```

Requires the target project to already have its own `package.json`
(run `npm init -y` first if it doesn't). Full walkthrough and every usage
example (Tailwind/shadcn, plain JS, Laravel Blade, the React scrollbar) live in
**[INSTALLATION.md](./INSTALLATION.md)**.

## Keeping projects updated

Made an edit to this preset (new token, new font, new logo, etc.)? Projects that
already installed it **won't** pick up the change automatically — GitHub installs
don't auto-update.

### If you're the one editing this preset

Push the change here first:
```bash
cd OJ-branding-preset
git add .
git commit -m "Describe what changed"
git push
```

### If you're using this preset in a project (and it's now outdated)

⚠️ **Before touching `node_modules`, commit or stash your own project's work first.**
```bash
git add .
git commit -m "WIP before updating oj-branding-preset"
```
This is just a safety net — reinstalling a package shouldn't normally touch your
own files, but committing first means you can always undo anything if a build
breaks or a path changes, instead of losing uncommitted work.

Then refresh the package:
```bash
npm uninstall oj-branding-preset
npm cache clean --force
npm install github:Wenoxxxx/OJ-branding-preset
```

The `npm cache clean --force` step matters — without it, npm can silently
serve the old cached version even after a fresh push.

After reinstalling, double-check nothing in your own code broke — e.g. a color
usage, an import path, or a component prop that changed — before committing
the update itself.

Full details, version bumping, and pinning to tags are in **[UPDATING.md](./UPDATING.md)**.

## Acknowledgements

Built on top of / designed to pair with:

- **[Tailwind CSS v4](https://tailwindcss.com)** — utility-first CSS framework the tokens are designed around
- **[shadcn/ui](https://ui.shadcn.com)** — component library these tokens/theme variables map onto
- **[tw-animate-css](https://github.com/Wombosvideo/tw-animate-css)** — animation utilities used alongside Tailwind
- **[React](https://react.dev)** — required as a peer dependency for the `CustomScrollbar` component
- **[Poppins](https://fonts.google.com/specimen/Poppins)** — brand UI font
- **[JetBrains Mono](https://www.jetbrains.com/lp/mono/)** — brand monospace font
- **npm / GitHub** — distribution method (`npm install github:...`)

## License

MIT