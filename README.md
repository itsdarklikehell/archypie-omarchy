# ArchyPie-Setup
A clone of RetroPie for Arch Linux Based Systems

# I am currently rewritting ArchyPie to bring it back into line with RetroPie. Along the way I have had to hack n' slash the code to get things working. After trying to make a port for Void Linux and adding back missing features into ArchyPie, as well as trying to get things working on the Raspberry Pi 5 it is clear a fresh start is required. Please continue to use the main branch for now and report any bugs you find. Thanks for trying ArchyPie, I hope to update the code soon.

## /omarchy integration (reference)

This repo is the upstream ArchyPie-Setup source. The /omarchy-side integration lives in
the `Omarchy-integration/` directory at the root of this tree:

- `Omarchy-integration/menu-integration.patch` — adds `install/gaming/archypie` to the
  Omarchy menu (`default/omarchy/omarchy-menu.jsonc`) and ships `default/applications/archypie.desktop`
  plus `bin/omarchy-install-gaming-archypie`.
- `Omarchy-integration/default/applications/archypie.desktop`
- `Omarchy-integration/bin/omarchy-install-gaming-archypie`
- `Omarchy-integration/manifest.json` + `README.md` — the Hermes plugin spec (see the
  `archypie-omarchy` skill).

### Layout rewrite

The install layout was rewritten to be /omarchy-compatible:

- `rootdir` stays `/opt/archypie` (system install).
- `datadir` moved from `~/ArchyPie` to `~/.local/share/archypie` (user data).
- `scriptmodules/supplementary/archypiemenu.sh` and related modules were updated for the new
  path. See commit `b26d4d2`.

## Packaging

A PKGBUILD is provided at `packages/archypie-setup/PKGBUILD`. Install it with:

```shell
cd packages/archypie-setup
makepkg -si
```

This installs the ArchyPie setup scripts to `/opt/archypie` and provides the `archypie-setup` command.

## Running the setup script

```shell
sudo pacman -Syyu
sudo pacman -S git
```

Then you can download the latest ArchyPie setup script with:

```shell
git clone --depth 1 https://github.com/V0rt3x667/ArchyPie-Setup.git
```

The script is executed with:

```shell
cd ArchyPie-Setup
sudo ./archypie_setup.sh
