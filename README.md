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

Once listed in the Obsidian community catalog, install **Transitrix Studio** from
Settings → Community plugins. The public distribution repository is
[transitrix/transitrix-studio-obsidian](https://github.com/transitrix/transitrix-studio-obsidian).

Demo notes with worked fences live in `demo/`.

## Privacy and safety

- Diagrams render as `<img>` with a `data:image/svg+xml` URL — YAML is never injected as HTML into the note DOM.
- Invalid or oversize fences show an in-place error panel instead of crashing the note.
- Source notes are never modified.

## License

MIT — see `LICENSE` in the repository root.
