# AGENTS.md

## Cursor Cloud specific instructions

This is a Jekyll + Gulp + SASS + BrowserSync static portfolio site ("Batu Projects").

### Runtime dependencies

Two runtimes are required:
- **Ruby 3.2+** with gems installed to `$HOME/.gems` (system Ruby from `apt`).
- **Node.js 6.x** via nvm (required for Gulp 3.x and node-sass 3.13.1 compatibility).

### Key gotchas

- The original `Gemfile.lock` pinned Jekyll 3.3.1 which is incompatible with Ruby 3.x (`URI.escape` removed, `safe_yaml` type errors). The lockfile was regenerated to resolve Jekyll 4.x and compatible gems. If the lockfile is reverted to the old versions, you must delete it and run `bundle install` again.
- `rexml` gem must be installed separately — it is not bundled with Ruby 3.2 by default but is required by kramdown/Jekyll.
- Gulp 3.x and node-sass 3.13.1 require Node.js 6.x. Higher Node versions will fail to build node-sass binaries or hit `graceful-fs` incompatibilities.
- Gems are installed to `$HOME/.gems` to avoid system permission issues. Always set `GEM_HOME=$HOME/.gems GEM_PATH=$HOME/.gems` when running Ruby/Jekyll/Bundler commands.

### Running the dev server

```bash
source ~/.nvm/nvm.sh && nvm use 6
GEM_HOME=$HOME/.gems GEM_PATH=$HOME/.gems PATH="$HOME/.gems/bin:$PATH" ./node_modules/.bin/gulp
```

This starts BrowserSync on `http://localhost:3000`, compiles SASS, builds with Jekyll, and watches for file changes.

### Build only (no dev server)

```bash
GEM_HOME=$HOME/.gems GEM_PATH=$HOME/.gems PATH="$HOME/.gems/bin:$PATH" jekyll build
```

### Lint / Test

No linter or test suite is configured (`npm test` exits with error by design). See `package.json` scripts section.
