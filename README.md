# Solenoid Properties

An Obsidian plugin that adds [Solenoid](https://solenoid-ngc.vercel.app)'s object types to a note's properties. A list, a matrix, a frame or a cube shows in the property row as the chip Solenoid draws for it, opens in Solenoid's table editor, and stays plain YAML in the note.

## Property types

| Type | YAML in the note | Chip |
|---|---|---|
| Numeric, String, Date, Complex and Boolean List | a sequence | `[N× List]` |
| Numeric, String, Date, Complex and Boolean Matrix | a sequence of sequences | `[R×C Table]` |
| Frame | a sequence of `key: value` maps | `[R×C Frame]` |
| Cube | a sequence of maps whose values may be lists or rows | `[R×C×D Cube]` |

Pick a type from the property's type menu, the way you would pick Number or Date. A key typed this way is recorded in `.obsidian/types.json` like any other.

```yaml
---
scores: [92, 85, 77]
grid:
  - [1, 2, 3]
  - [4, 5, 6]
orders:
  - { item: Widget, qty: 3, due: 2026-10-01 }
  - { item: Gasket, qty: 12, due: 2026-10-04 }
---
```

The editor is the app's own: cell and header editing, add and remove rows and columns, a column type cycle, sort, a CSV view, copy as Markdown, export CSV, a summary footer, and drill-in for a cube. Save writes the value back as YAML. Dates are ISO text in the note. A frame row is written with every key, and a cell that has no value is `null`.

What a note cannot hold is left out: formula columns, units and per-column formats need a graph. Solenoid reads a list or a frame the plugin writes as the same type; a matrix arrives as a text list until Solenoid's note reader types matrices.

## Settings

One setting: the color palette, chosen from Solenoid's built-in palettes. Light and dark follow Obsidian's theme.

## Install

From Obsidian's community plugin list, once the listing is accepted. Until then, either:

- [BRAT](https://github.com/TfTHacker/obsidian42-brat): add `bubba8587/Solenoid-Properties` as a beta plugin.
- By hand: download `main.js`, `manifest.json` and `styles.css` from the [latest release](https://github.com/bubba8587/Solenoid-Properties/releases/latest) into `<vault>/.obsidian/plugins/solenoid-properties/`, then enable the plugin under Settings → Community plugins.

## Source and build

This repository holds the manifest and the releases. The plugin's source is the `obsidian-plugin/` folder of [bubba8587/solenoid](https://github.com/bubba8587/solenoid), because the chips and editors are the app's own React components, bundled by a plugin-only Vite build (`npm run plugin:build`) behind a short list of module shims. The mechanics, the type table and every place the plugin differs from the app are in [`specs/obsidian-plugin.md`](https://github.com/bubba8587/solenoid/blob/develop/specs/obsidian-plugin.md) there.

`source.json` names the Solenoid commit a release is built from. The release workflow checks that commit out, builds it, and attaches `main.js`, `manifest.json`, `styles.css` and `third-party-licenses.txt` to the release. It refuses to publish when this repository's `manifest.json` differs from the one at the pinned commit.

## Releasing

1. In `bubba8587/solenoid`, set the version in `obsidian-plugin/manifest.json` and push.
2. Here, set `source.json`'s `ref` to that commit, copy the manifest over, add the version to `versions.json` with its `minAppVersion`, and push.
3. Create the release: push a tag equal to the version (`0.1.0`, no `v`), or open Actions → Release → Run workflow and type the version. The workflow builds and attaches the files.

The community listing is submitted once, through [community.obsidian.md](https://community.obsidian.md) (sign in, link GitHub, add this repository). Its automated review scans every published release after that, so a release is never left as a draft.

## License

MIT. The bundle's third-party licenses (React, chrono-node, PapaParse, the Atkinson Hyperlegible fonts) ship with each release as `third-party-licenses.txt`.
