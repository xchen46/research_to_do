# Research To-Do Board

A weekly to-do board in a single HTML file. It needs no install, no account and no server.

- **Week by week.** Every task belongs to a week (Mon–Sun). Anything left unfinished rolls into the next week automatically and is tagged "carried N wks".
- **Lists.** Tasks are grouped into lists (e.g. "Patagium — code", "Writing & deadlines").
- **Subtasks.** A big task can hold steps, with optional section headings. Two progress bars: **Tasks** counts whole tasks, and **Items** counts every subtask.
- **Import from Markdown.** Drop in a `.md` to-do list. `- [ ]` / `- [x]` checkboxes, `## headings` and numbered lists are understood. A file whose first line is a single `# Title` can come in as one task with steps. Re-importing the same file only adds what's new and ticks off newly checked items.
- **Click to edit.** Clicking the checkbox ticks the task off. Clicking the text opens it, so you can rename it, move it to another list or week, or edit its steps.

## Use it

**Option 1: open the file.** Download `index.html` and double-click it. That's it.

**Option 2: host it on GitHub Pages** (gives you a link you can bookmark):

1. Fork this repo (or upload `index.html` to a new repo).
2. Go to **Settings → Pages**, set *Source* to **Deploy from a branch**, branch `main`, folder `/ (root)`, then click **Save**.
3. After a minute your board is live at `https://<your-username>.github.io/<repo-name>/`.

**Option 3: host it yourself.** It's a single static file, so anything that serves files works.

- *On your own computer* (gives you a stable address like `http://localhost:8000`):
  ```bash
  git clone https://github.com/<your-username>/<repo-name>.git
  cd <repo-name>
  python3 -m http.server 8000      # or: npx serve .
  ```
  Then open <http://localhost:8000> in your browser. Stop the server with `Ctrl+C`.
- *On a server or another host:* copy `index.html` to any static web host (Netlify, Cloudflare Pages, a university web space, nginx/Apache). No build step and no backend are needed.

Note: the browser stores the board per address. A board you used at `file://…/index.html` won't show up at `http://localhost:8000` or on your GitHub Pages link, and vice versa. Use **Save backup / Restore backup** to move it between them, and stick to one address (and port) for everyday use.

## Where your data lives

Tasks are saved in **your browser's local storage** on the device you're using. That means:

- Each person who opens the page gets their own empty board. Nobody can see anyone else's tasks.
- Clearing browser data, or using a private window, wipes the board.
- To move a board to another computer or browser, use **Backup → Save backup** (a `.json` file), then **Restore backup** on the other device. Make a backup now and then.

## Markdown import format

See [`example-todo.md`](example-todo.md). In short:

```markdown
# Cell-level derivation          ← optional title: import as ONE task with steps
## A. Agent → kinetic equation   ← section heading
- [ ] State the drift and noise
- [x] Itô on φ(X_t)              ← [x] = already done
## B. Moments
1. 0th moment → continuity eq.   ← numbered lists work too
   - check boundary terms        ← indented items attach to the one above
```

Without a `# Title`, each `## heading` becomes a list and each bullet becomes its own task. You can switch between "One task with steps" and "Separate tasks" before you click Add.

## Make it yours

Everything is in `index.html`: the styles at the top, the logic at the bottom.

| Want to change… | Look for |
|---|---|
| Colors (light and dark) | the `:root{ --bg … --accent … }` blocks at the top of `<style>` |
| Fonts | the Google Fonts `<link>` and `--display / --body / --mono` |
| Week start day (Monday by default) | `function weekKey` (`(d.getDay()+6)%7` means Monday) |
| How Markdown is read | `function parseMd` |
| How the progress bars count | `function units` and `function subCounts` |
| Where data is stored | `function makeLocalDB` (swap it for Firebase, Supabase, etc. to sync across devices; it only needs `add`, `doc(id).update/delete` and `onSnapshot`) |

## About

Built by Harry Chen to keep track of research to-dos week by week. The code was generated with Claude (Anthropic's AI assistant) through conversation, then tested and adjusted. Feel free to fork it and make it your own.

## License

MIT. Use it, change it, share it.
