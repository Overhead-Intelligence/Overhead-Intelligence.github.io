# Overhead-Intelligence.github.io

Static-site host for **interactive diagrams and visualizations embedded in the OI Notion wiki**.

Live at: https://overhead-intelligence.github.io/

## Structure

This is a single GitHub Pages deployment serving multiple pages, one per folder:

```
/                       → landing page (lists available diagrams)
/architecture/          → system-at-a-glance diagram
/<future-diagram>/      → add new diagrams as new folders
```

GitHub Pages serves the entire repo tree from `main`. Push a folder containing an `index.html`, and it's live at the matching subpath within ~60 seconds.

## Adding a New Diagram

1. Create a new folder at the repo root, e.g. `network-topology/`.
2. Add an `index.html` (self-contained — inline CSS/JS, no build step).
3. Add a card linking to it in the root `index.html` under the "Available Pages" grid.
4. Commit and push to `main`. GitHub Pages redeploys automatically.
5. In Notion, type `/embed` and paste `https://overhead-intelligence.github.io/<folder>/`.

### Diagram conventions

- **Self-contained HTML.** Inline CSS and JS. No bundlers, no npm. If you need a library, prefer a CDN script tag.
- **Dark theme palette** (matches the rest of the wiki visuals):
  - `--bg: #0f1419` — page background
  - `--panel: #21262d` — component fill
  - `--border: #30363d` — default stroke
  - `--accent: #58a6ff` — highlights, hover states, links
  - `--text: #e6edf3` / `--text-dim: #7d8590`
- **Links to Notion pages** must use `target="_top"` so clicks navigate the parent Notion view rather than the iframe.
- **Tooltips** on hover are preferred over alt-text or static labels for component details.

## Public-Facing — Don't Publish Sensitive Data

This is a **public** repo and a **public** website. Anything pushed here is reachable by anyone with the URL. Do not include:

- Operational RF frequencies or hopping schedules
- Internal IP schemes, hostnames, or VPN topology details
- Customer names, project codenames, or mission specifics
- Hardware serial numbers or asset IDs
- Tailscale auth keys, API tokens, or any credentials

If a diagram needs to show sensitive details, host it privately (e.g. on a Tailscale-fronted box or behind the VPN) and embed via that private URL instead.

## Local Preview

```bash
cd <folder>
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open the `index.html` file directly in a browser — relative paths and inline assets work without a server.
