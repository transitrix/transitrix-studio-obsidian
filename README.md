# Transitrix Studio

> **Distribution repository** for the Obsidian Desktop plugin.
> Source of truth, build and tests live in [`transitrix/transitrix-studio`](https://github.com/transitrix/transitrix-studio)
> (`packages/obsidian-plugin`). `main.js` is attached to each GitHub Release here
> and its release note links the exact source commit. Please open issues and
> pull requests against the monorepo.

Preview **self-contained** Transitrix diagram YAML as SVG inside Obsidian Desktop notes (Reading view).

The plugin reuses the Studio parser, validator, and SVG renderer. It does not walk the vault, call network APIs, or rewrite notes.

## Requirements

- Obsidian Desktop 1.0.0 or newer (`isDesktopOnly`)
- Restricted mode off so community plugins can load

## Supported fences

| Language | Diagram |
| --- | --- |
| `transitrix-goals` | Goals tree |
| `transitrix-dgca` | DGCA chain |
| `transitrix-dga` | DGA chain |
| `transitrix-action` | Action network (PSND) |
| `transitrix-action-card` | Action Card (shell + milestones) |
| `transitrix-blocks` | Nested blocks or grid (for example RACI) |
| `transitrix-process-blueprint` | Process Blueprint |

Example:

````markdown
```transitrix-goals
notation: goals
spec_version: "0.1"
id: GOALS-SERVICE-1
name: Reliable service
goal_types:
  - { name: Strategy, level: 0 }
goals:
  - { id: GOAL-SERVICE-1, name: Deliver reliable service, type: Strategy, level: 0 }
```
````

Open the note in **Reading view** to see the SVG. Live Preview is not supported yet.

Repository projections (`view_config`-only documents or `sources`) are rejected. Put a self-contained document in the fence.

## Settings

**Settings → Transitrix Studio**

| Setting | Effect |
| --- | --- |
| Theme | Transitrix light / dark, or follow Obsidian |
| Node size | compact / normal / wide |
| Edge style | straight / bezier / polyline (Goals, DGCA, DGA) |
| Edge curvature | 0–3 (Goals, DGCA/DGA, Action) |

Action Card uses Theme only. Changing settings refreshes open Reading-view diagrams.

## Install

### From the community catalog

Once listed in the Obsidian community catalog, install **Transitrix Studio** from
Settings → Community plugins. The public distribution repository is
[transitrix/transitrix-studio-obsidian](https://github.com/transitrix/transitrix-studio-obsidian).

### Manual install (until the plugin is in the catalog)

Obsidian Desktop only.

1. Open the [latest release](https://github.com/transitrix/transitrix-studio-obsidian/releases/latest)
   and download the three files listed under **Assets**: `main.js`,
   `manifest.json` and `styles.css`. Do not use "Source code (zip)" — it does not
   contain `main.js`.
2. In your vault, create the folder `.obsidian/plugins/transitrix-studio/`. The
   folder name must be exactly `transitrix-studio`. `.obsidian` is hidden in most
   file managers; show hidden files or create the folder from a terminal.
3. Copy the three downloaded files into that folder.
4. In Obsidian open Settings → Community plugins, turn **Restricted mode** off,
   click the refresh icon next to "Installed plugins", and enable
   **Transitrix Studio**.
5. Open a note with a `transitrix-*` fence in **Reading view**.

To update, download the three files from the newer release, overwrite the old
ones and restart Obsidian (or disable and re-enable the plugin).

Optional: the release notes list a SHA-256 for each file. Compare it with the
file you downloaded (`Get-FileHash main.js` on Windows, `shasum -a 256 main.js`
on macOS/Linux).

Demo notes with worked fences live in `demo/`.

## Privacy and safety

- Diagrams render as `<img>` with a `data:image/svg+xml` URL — YAML is never injected as HTML into the note DOM.
- Invalid or oversize fences show an in-place error panel instead of crashing the note.
- Source notes are never modified.

## License

MIT — see `LICENSE` in the repository root.
