# Solenoid Properties

An Obsidian plugin that adds [Solenoid](https://solenoid-ngc.vercel.app)'s objects to the available property types, wraps them in clickable buttons, and adds Solenoid's pop-up editor for easy entry + management of tabular data inside your frontmatter.

![A note's properties shown as Solenoid chips: lists, a table, a frame and a cube](https://raw.githubusercontent.com/bubba8587/Solenoid-Properties/main/images/1.png)

The plugin also ships a theme to make your Obsidian vault look and feel like Solenoid! (Default palette only.) Enable it in the plugin settings.

![An Obsidian vault wearing the Solenoid look](https://raw.githubusercontent.com/bubba8587/Solenoid-Properties/main/images/3.png)

## Property types

| Type                                                | Description                                                                                               | Chip           |
| --------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | -------------- |
| Numeric, String, Date, Complex and Boolean **List** | A 1-D *row* of data. Same format as Obsidian's mixed List, but restricted to one data type.               | `[N× List]`    |
| Num, Str, Date, Cx Bool **Matrix**                  | A 2-D data set. One data type.                                                                            | `[R×C Table]`  |
| Frame                                               | Analogous to `pandas` dataframe. A set of data columns, with headers. Each column can have one data type. | `[R×C Frame]`  |
| Cube                                                | Like the Frame, but can contain all other object types in its cells for nested data.                      | `[R×C×D Cube]` |

![The pop-up editor open on a text list](https://raw.githubusercontent.com/bubba8587/Solenoid-Properties/main/images/2.png)

Solenoid Property objects save as block-style YAML:

```yaml
---
scores:
  - 92
  - 85
  - 77
grid:
  - - 1
    - 2
    - 3
  - - 4
    - 5
    - 6
orders:
  - item: Widget
    qty: 3
    due: 2026-10-01
  - item: Gasket
    qty: 12
    due: 2026-10-04
---
```

![Solenoid importing the same note, each property on its own typed socket](https://raw.githubusercontent.com/bubba8587/Solenoid-Properties/main/images/4.png)

**Note on existing bug:** A Frame's per-column types are stored in the plugin's `data.json` for better YAML parseability and these are not currently forwarded to the main app, which may guess the data type incorrectly. This will be fixed in the next bugfix release.

## Disclosures

- **Clipboard:** the pop-up editor's Copy, Copy as Markdown and copy-cell actions write to the system clipboard when you use them. The plugin never reads the clipboard.
- **No network access, no telemetry.** The plugin's settings and a Frame's column types are kept in the plugin's own `data.json`.

## Source

The source in `src/` and `obsidian-plugin/` is a snapshot exported from [bubba8587/solenoid](https://github.com/bubba8587/solenoid), where the plugin is developed, because the chips and editors are Solenoid's own components; `source.json` names the commit. `npm ci && npm run build` builds `dist/` from it, and each release's files carry a GitHub build provenance attestation.

## License

MIT. The bundle's third-party licenses (React, chrono-node, PapaParse, the Atkinson Hyperlegible fonts) are in [`THIRD-PARTY-LICENSES.txt`](THIRD-PARTY-LICENSES.txt).
