# Updating

See also: **[README.md](./README.md)** for the project overview, and
**[INSTALLATION.md](./INSTALLATION.md)** for first-time setup and usage examples.

There are two sides to this: pushing a change to this repo, and pulling that
change into a project that already installed it.

## 1. Pushing a change (maintainer side)

Whenever you add a folder/file, edit a token, or change a component:

```bash
cd OJ-branding-preset

# make your changes (new files, edited tokens, etc.)

npm version patch
# bumps the version in package.json, e.g. 1.0.0 → 1.0.1
# also creates a git tag automatically

git add .
git commit -m "Describe what changed"
git push
git push --tags
```

Use `npm version minor` instead of `patch` for a bigger addition (new component,
new token category), and `npm version major` for a breaking change (renamed
tokens, removed exports).

## 2. Pulling the update into a project (consumer side)

⚠️ **Before touching `node_modules`, commit or stash your own project's work first.**
```bash
git add .
git commit -m "WIP before updating oj-branding-preset"
```
This is just a safety net — reinstalling a package shouldn't normally touch your
own files, but committing first means you can always undo anything if a build
breaks or a path changes, instead of losing uncommitted work.

The GitHub-install method doesn't track versions the way registry packages do,
so a plain `npm update` is unreliable here. The safe way is uninstall + reinstall:

```bash
cd your-project

npm uninstall oj-branding-preset
npm cache clean --force
npm install github:Wenoxxxx/OJ-branding-preset
```

The `npm cache clean --force` step matters — npm sometimes caches the GitHub
tarball by commit, so without clearing it, a plain reinstall can silently give
you the old version even after you pushed new changes.

After reinstalling, double-check nothing in your own code broke — e.g. a color
usage, an import path, or a component prop that changed — before committing
the update itself.

## 3. Verify the update actually came through

```bash
dir node_modules\oj-branding-preset        # Windows
ls node_modules/oj-branding-preset          # Mac/Linux
```

Check that your newly added folder/file shows up, or that an edited token
file reflects the new value.

## Pinning to a specific version

Once a version is stable and you don't want a project to auto-pull future
changes, install a specific tag instead of the latest `main` branch:

```bash
npm install github:Wenoxxxx/OJ-branding-preset#v1.0.1
```

## Note on going further

This uninstall/reinstall dance is the tradeoff of the GitHub-install method —
no proper semver tracking, no automatic `npm update`. If this becomes annoying
across many projects, the alternative is publishing to the actual npm registry
under a scoped name (e.g. `@wenoxxxx/oj-branding-preset`), which supports real
`npm update`. That requires resolving the npm 2FA/access-token setup once.

---

For installation steps, prerequisites, and per-platform usage (Tailwind/shadcn,
plain JS, Laravel Blade, fonts, logos), see **[INSTALLATION.md](./INSTALLATION.md)**.
For the project overview and folder structure, see **[README.md](./README.md)**.