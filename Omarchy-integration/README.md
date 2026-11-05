# ArchyPie on Omarchy — Hermes plugin spec

This is the plugin spec for packaging the ArchyPie ↔ /omarchy work into a
Hermes plugin so the dev team can use the skills and read-only helpers from the
agent loop.

## Files

```
plugins/archypie-omarchy/
├── manifest.json          # plugin metadata (id, version, description)
├── SKILL.md               # the archypie-omarchy skill
├── README.md              # how to install and use the plugin
└── scripts/
    ├── archypie-menu-check   # report installed/available state
    └── archypie-dev-tasks    # print current task-board ids (T1-T5)
```

## Sample tool: `archypie-menu-check`

A tiny Bash tool that reports whether ArchyPie is already installed on the
/omarchy machine (for the `disabled` guard on the menu row):

```bash
#!/usr/bin/env bash
# archypie-menu-check — report ArchyPie install state.
ROOT="/opt/archypie"
DATA="${HOME}/.local/share/archypie"

if [[ -f "${ROOT}/archypie_setup.sh" ]] || [[ -d "${DATA}" ]]; then
    echo "installed"
else
    echo "not-installed"
fi
```

## Installing

1. Copy this folder to `~/.hermes/plugins/archypie-omarchy/`.
2. Enable it via the plugin UI or `muse_manage plugin enable archypie-omarchy`.
3. Restart the shell.

## Safety

- The plugin adds read-only helpers. It never edits the user's Omarchy config;
  only a review-led PR does that.
- A plugin that writes to `~/.config/omarchy/extensions/` is out of scope for
  the first release.
