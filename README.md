# Oklahoma State Society of Artificial Intelligence (OSSAI)

Founding and registration tracker for OSSAI at Oklahoma State University.

**Live site:** enable GitHub Pages on this repo (Settings → Pages → Deploy from branch → `main` / root).

## What's here

| Path | What it is |
| --- | --- |
| `index.html` | The whole app — plan, live-synced checklist, PERT dependency chart, curriculum. No build step. |
| `club-info.json` | Canonical facts: registration requirements, key dates, blockers, framework pillars. |
| `content/curriculum.md` | The four pillars, learning library, skills, tools, applications. |
| `content/talk-outline-ai-what-i-have-learned.md` | Full talk outline — candidate flagship Safety & Alignment session. |

## How the app works

Everything is driven by two arrays near the top of the `<script>` block in `index.html`:

- **`GROUPS`** — checklist sections. Each item has an `id`, display `text`, and a `pert` key naming the graph node it feeds.
- **`PERT_NODES` / `PERT_EDGES`** — the dependency graph. Each node declares a `checklist: []` array of item ids that must *all* be checked for that node to count as complete.

That cross-reference is the whole trick: check a box and the PERT chart recolors itself. Nothing is kept in sync by hand.

To add a task, add it to the right `GROUPS` entry and point its `pert` key at a node. To add a stage, add a node plus its edges.

## Setup

The app needs a Firebase project so every officer sees the same checklist state.

1. Create a project at [console.firebase.google.com](https://console.firebase.google.com)
2. Enable **Firestore Database**
3. Copy the web app's `firebaseConfig`
4. Replace the placeholder block in `index.html` (search for `YOUR_API_KEY`)

Until that's done the site shows a setup overlay with the same instructions and runs read-only.

State lives in a single Firestore document: `ossai/checklist`, a flat `{ itemId: boolean }` map.

> **Security note:** Firestore's "test mode" leaves the database readable and writable by anyone with the URL. Tighten the security rules before sharing this site beyond the officer group.

## Status

Pre-registration. The critical path is SGA approval via CampusLink — funding, room booking, and an official Involvement Fair table are all blocked behind it, and the approval turnaround is currently unknown.
