# me.proton.Meet — Proton Meet (community Flatpak)

> **Unofficial community packaging.** This Flatpak is not provided or supported by Proton AG.

Proton Meet is an end-to-end encrypted video conferencing client from Proton AG.
This repo packages the `applications/meet-desktop` Electron workspace from the
[ProtonMail/WebClients](https://github.com/ProtonMail/WebClients) monorepo as a
standalone Flatpak.

---

## Install

### From a GitHub Release bundle (recommended)

1. Check your architecture if unsure: `uname -m`
2. Download the correct bundle from the [latest release](../../releases/latest):

| Architecture | File |
|---|---|
| x86_64 (most desktops/laptops) | `me.proton.Meet.flatpak` |
| aarch64 / arm64 | `me.proton.Meet-aarch64.flatpak` |

3. Install it:

```sh
# x86_64
flatpak install --user me.proton.Meet.flatpak

# aarch64
flatpak install --user me.proton.Meet-aarch64.flatpak
```

4. Run it:

```sh
flatpak run me.proton.Meet
```

---

## Automation pipeline

| Workflow | Trigger | What it does |
|---|---|---|
| `flatpak-external-data-checker` | Weekly (Sunday 00:00 UTC) | Detects new `proton-meet@x.y.z.w` upstream tags; opens a PR bumping `me.proton.Meet.yml` |
| `update-generated-sources` | Push to `main` touching the manifest | Clones WebClients at the new tag, strips private-registry stanzas, runs `flatpak-node-generator`, opens a PR updating `generated-sources.json` |
| `build` | Push to `main` touching the manifest or generated-sources | Builds the Flatpak for **x86_64** and **aarch64** in parallel with `flatpak-builder` and publishes a GitHub Release with both `.flatpak` bundles |

---

## Regenerating `generated-sources.json` locally

```sh
# Requires: pip install flatpak-node-generator
./update-generated-sources.sh
```

Or, to target a specific upstream tag:

```sh
./update-generated-sources.sh proton-meet@0.4.17.0
```

---

## License

The Flatpak packaging files in this repo are released under [MIT](LICENSE).
The upstream Proton Meet application is licensed under [GPL-3.0-only](https://github.com/ProtonMail/WebClients/blob/main/LICENSE).
