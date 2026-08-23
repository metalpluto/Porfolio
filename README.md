# dhruv.dev Terminal Portfolio

A single-file, terminal-styled personal portfolio site. No build step, no framework, no dependencies just one `portfolio.html` you can open directly in a browser or deploy anywhere static files are served

The whole site is themed as an interactive terminal: visitors type commands to explore your bio, skills, and projects, while a traditional scrollable "below-the-fold" version of the same content sits underneath for anyone who just wants to scroll

---

## Features

### Interactive terminal
- A fully working fake shell (`visitor@dhruv.dev:~$`) that accepts typed commands
- Command history — cycle through previously entered commands with **↑ / ↓**
- Tab-completion for every command, theme name, and sound name
- Blinking, glowing custom cursor that repositions itself as you type
- `Ctrl + L` clears the terminal (standard shell shortcut)
- Click anywhere in the terminal window to focus the input

### Commands
| Command | What it does |
|---|---|
| `about` | Bio, title, location, email, GitHub — rendered in a bordered box |
| `skills` | Technical skills grouped by category |
| `projects` | Lists your projects inline in the terminal |
| `theme` / `theme <name>` | Cycles or sets a color theme |
| `sound` / `sound <name>` / `sound on` / `sound off` / `sound list` | Toggles keystroke sound, or switches sound style |
| `clear` | Clears the terminal output |
| `banner` | Prints the ASCII-art name banner |
| `whoami` | Prints the current user string |
| `date` | Prints the current date/time |
| `ping` | Fake latency check, for fun |
| `history` | Shows the last 20 commands you've typed |
| `neofetch` | System-info-style summary card (OS, browser, resolution, theme, sound, uptime) |
| `scroll <section>` | Smooth-scrolls to `about`, `skills`, or `projects` below the fold |

A live reference list of all commands is shown in a sidebar panel to the left of the terminal (on wide screens).

### Themes
5 built-in color themes, switchable live with `theme <name>`:
- `cyber` (default)
- `nord`
- `solarized`
- `dracula`
- `bloodwork`

Each theme also has its own distinct **cursor animation style** (glow pulse, hard blink, heartbeat pulse, etc). Your chosen theme is saved in `localStorage` and persists across visits

### Keystroke sounds
10 selectable keyboard sound profiles, generated live with the Web Audio API (no audio files needed):

`mech` · `soft` · `typewriter` · `synth` · `arcade` · `laser` · `bubble` · `wood` · `glass` · `drum`

- `sound` — toggle on/off
- `sound <name>` — switch style (previews it immediately)
- `sound list` — show all available styles and which one is active
- Preference is saved in `localStorage`

### Live GitHub activity panel
An independent widget on the right side of the hero section that shows your recent public GitHub activity in real time pushes, commits, PRs, issues, comments, stars, forks, releases, and more pulled from GitHub's public Events API. No login or token required. Auto-refreshes every 60 seconds.

Because it reads GitHub's public activity feed, it doesn't matter whether you pushed from VS Code, the terminal, or GitHub.com directly it all shows up the same way

### Auto-populated Projects section
The "Projects" section (both in the terminal `projects` command and the scrollable page below) can pull live from your public GitHub repos instead of being hand-written.

**How it works:**
- Repos tagged with the GitHub topic `portfolio` are automatically shown as projects
- Forked repos are always excluded
- The repo's **About → Description** becomes the project's write-up
- Any other **topics** on the repo become its tech-stack tags (falls back to the repo's primary language if none are set)
- The repo's **Website** field (if set) becomes the "Live →" link
- Refreshes automatically every 5 minutes
- If no tagged repos are found (or the fetch fails), the site falls back to the hand-written project list in `CONFIG.projects` — nothing breaks

To feature a project: on GitHub, open the repo → the gear icon next to **About** → add a description, add the topic `portfolio` (plus any tech-stack topics you like) → save

### Below-the-fold sections
A traditional scrollable layout mirrors the terminal content for accessibility and for visitors who prefer scrolling to typing:
- **About** — bio paragraphs + meta info
- **Skills** — categorized skill cards
- **Projects** — card grid (same data source as the `projects` command)

### Design & UX details
- Fully responsive; side panels (command reference + GitHub activity) hide on narrower screens and the terminal centers itself
- Custom scrollbars styled to match the active theme
- Ambient background effects and a mouse-following glow
- Sticky, blurred navigation bar with smooth-scroll links
- No external JS frameworks — vanilla HTML/CSS/JS in a single file

---

## 🛠 Configuration

Nearly everything personal lives in one place — the `CONFIG` object near the top of the `<script>` block:

```js
var CONFIG = {
  name:     'Your Name',
  title:    'Your Title',
  location: 'Your Location',
  email:    'you@example.com',
  github:   'your-github-username',
  summary:  '...',
  skills:   { /* category: [skills] */ },
  projects: [ /* fallback projects, used if GitHub auto-fetch finds nothing */ ]
};
```

Two additional constants control the live GitHub integrations (found near the bottom of the file, in their own `<script>` blocks):

```js
var GH_USER = CONFIG.github;      // GitHub username to watch
var GH_PROJECT_TOPIC = 'portfolio'; // topic tag that marks a repo as a "project"
```

---

## Deployment

This is a single static HTML file — deploy it anywhere that serves static files:
- **GitHub Pages** — push `portfolio.html` (rename to `index.html`) to a repo and enable Pages
- **Vercel / Netlify** — drag and drop, or connect the repo
- **Any web host / VPS** — just upload the file

No build step, no `npm install`, no server required

---

## License

MIT see [LICENSE]