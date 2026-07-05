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

## Quick install

```bash
npm install github:Wenoxxxx/OJ-branding-preset
```

Requires the target project to already have its own `package.json`
(run `npm init -y` first if it doesn't). Full walkthrough and every usage
example (Tailwind/shadcn, plain JS, Laravel Blade, the React scrollbar) live in
**[INSTALLATION.md](./INSTALLATION.md)**.

## Updating

Changed a token or added a new file? See **[UPDATING.md](./UPDATING.md)** for
how to push the change and how to refresh it in projects that already installed it.

## License

MIT