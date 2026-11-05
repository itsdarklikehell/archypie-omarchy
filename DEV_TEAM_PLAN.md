# ArchyPie ↔ /omarchy port — dev team plan

## Goal
Turn ArchyPie-Setup from a stand-alone RetroPie clone into a first-class
/omarchy experience: ship under `Install > Gaming`, install as an Arch package,
and keep the existing `dialog` module system working.

## The three integration levels (done before merging anything)

1. **Menu entry** — add `install.gaming.archypie` to the Omarchy menu JSONC
   (`default/omarchy/omarchy-menu.jsonc` for the PR; `~/.config/omarchy/extensions/`
   for a local test). No code changes needed in ArchyPie.
2. **Package install** — a PKGBUILD for ArchyPie itself, surfaced by
   `bin/omarchy-install-gaming-archypie` so the menu row greys out when installed
   (`omarchy-pkg-present`).
3. **Layout rewrite** — move `datadir` from `~/ArchyPie` to
   `~/.local/share/archypie` and keep `rootdir=/opt/archypie`, matching the
   /omarchy layout convention.

## Recommended team shape (one lead + three owners)

| Role | Owner | Scope | Deliverable |
|---|---|---|---|
| **Lead** | Aino (Arlecchino) | merge gate, JSONC + PKGBUILD ownership, PR hygiene | `menu-integration.patch` reviewed and merged |
| **Arch compatibility** | Raiden Shogun | rewrite `datadir`/`configdir` to the /omarchy layout; test on a clean Arch install | patched `archypie_packages.sh`, `scriptmodules/*.sh` |
| **Menu integration** | Fiona | desktop file + install script + JSONC entry | `default/applications/archypie.desktop`, `bin/omarchy-install-gaming-archypie` |
| **E2E mentor** | Venti | headless full-installer run on /omarchy, gates merges | install log + `logs/` results |

## Suggested task board

1. **T1** — Port layout (`datadir` → `~/.local/share/archypie`), keep rootdir.
2. **T2** — Add `install/gaming/archypie` menu entry + desktop file.
3. **T3** — PKGBUILD for ArchyPie (binary/source), wire into Omarchy install script.
4. **T4** — E2E: run `setup gui` headless on /omarchy, fix dialogs, verify modules.
5. **T5** — Update README + skill docs, open PR.

## How to hand off to an owner

Each owner works on their own branch in the ArchyPie-Setup repo, then opens a
PR for their piece. The lead merges T1+T2+T3 as one PR into `main`, runs T4,
then opens the Omarchy-side PR.

## Notes

- The `scriptmodules/supplementary/` modules themselves should keep working
  unchanged; the port is about paths, the install flow, and the UI.
- Dialogs are `sudo`-driven: always test under `sudo ./archypie_setup.sh`.
- The `admin/setup.sh` module is the highest-risk file for platform-specific
  paths; give it the most review time.
