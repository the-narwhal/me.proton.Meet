# me.proton.Meet — Proton Meet (community Flatpak)

> **Unofficial community packaging.** This Flatpak is not provided or supported by Proton AG.

Proton Meet is an end-to-end encrypted video conferencing client from Proton AG.
This repo packages the `applications/meet-desktop` Electron workspace from the
[ProtonMail/WebClients](https://github.com/ProtonMail/WebClients) monorepo as a
standalone Flatpak.

---

## Install

### From a GitHub Release bundle (recommended)

1. Download `me.proton.Meet.flatpak` from the [latest release](../../releases/latest).
2. Install it:

```sh
flatpak install --user me.proton.Meet.flatpak
```

3. Run it:

```sh
flatpak run me.proton.Meet
```

---

## Automation pipeline

| Workflow | Trigger | What it does |
|---|---|---|
| `flatpak-external-data-checker` | Weekly (Sunday 00:00 UTC) | Detects new `proton-meet@x.y.z.w` upstream tags; opens a PR bumping `me.proton.Meet.yml` |
| `update-generated-sources` | Push to `main` touching the manifest | Clones WebClients at the new tag, strips private-registry stanzas, runs `flatpak-node-generator`, opens a PR updating `generated-sources.json` |
| `build` | Push to `main` touching the manifest or generated-sources | Builds the Flatpak with `flatpak-builder` and publishes a GitHub Release with the `.flatpak` bundle |

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
