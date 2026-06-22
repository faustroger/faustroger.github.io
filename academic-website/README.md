# Roger Faust — Academic Website (living-CV system)

A clean, fast, tenure-track-ready academic site that you maintain by editing **one file**: `content.yml`. No build step, no framework, no command line required after setup. It deploys free on GitHub Pages.

The design principle: **you should never have to touch code to update your site.** Add a publication, a talk, an outreach event, or a field note by copying a short template into `content.yml`, committing, and you're live in about a minute.

---

## What's in this folder

| File | What it is | Do you edit it? |
|---|---|---|
| `content.yml` | **All your content.** Profile, about, research, teaching, contact, and the dated entry stream. | **Yes — this is the only file you edit.** |
| `index.html` | The site engine. Reads `content.yml` and renders every page. | Rarely / never |
| `assets/` | Your photo, CV PDF, and field-note images. | Add files here |
| `.nojekyll` | Tells GitHub Pages to serve files as-is. | No |
| `update-reminder.ics` | A ready-to-import recurring calendar reminder (every 5 weeks). | Import once |
| `.github/workflows/update-reminder.yml.optional` | Optional GitHub-based backup reminder. | Optional |

---

## How the site is structured

Pages: **Home · About · Research · Publications · Teaching · Outreach/Engagement · Photos/Field Notes · Contact.**

There are two kinds of content in `content.yml`:

1. **Profile blocks** (slow-changing): your bio, research areas, courses, contact info. Edit these once in a while.
2. **Entries** (your living CV): a single growing list at the bottom of the file. Each publication, talk, outreach event, and field note is one entry with `date`, `type`, `title` (and optional `venue`, `description`, `links`, `tags`). The site automatically files each entry into the right page and sorts by date — publications are even auto-grouped by year. The Home page shows your five most recent entries as a "Recent updates" feed.

That's the whole system. You grow the entry list over the years; the site reorganizes itself.

---

## Part 1 — Deploy on GitHub Pages (one-time, ~10 minutes)

You only do this once. After that, updating is just editing `content.yml` in your browser.

1. **Create a free GitHub account** at <https://github.com> if you don't have one.
2. **Create a new repository.**
   - For a personal site at `https://YOURUSERNAME.github.io`, name the repo exactly `YOURUSERNAME.github.io`.
   - Or name it anything (e.g. `website`) to get `https://YOURUSERNAME.github.io/website/`.
   - Set it to **Public**. (Replace `YOURUSERNAME` with your real username everywhere below.)
3. **Upload these files.** On the new repo page click **Add file → Upload files**, then drag in everything from this folder: `index.html`, `content.yml`, `.nojekyll`, the `assets/` folder, and (optionally) the `.github/` folder. Click **Commit changes**.
   - Note: `.github` and `.nojekyll` start with a dot. They'll upload fine via drag-and-drop; if your file picker hides them, drag the whole folder in instead.
4. **Turn on Pages.** Repo **Settings → Pages**. Under "Build and deployment", set **Source = Deploy from a branch**, **Branch = main**, **Folder = / (root)**. Click **Save**.
5. **Wait ~1–2 minutes**, then visit your URL (shown on that Settings → Pages screen). Done.

> If you see the "Could not load content.yml" message when double-clicking `index.html` on your own computer, that's expected — browsers block local file reads. It works correctly once it's on GitHub Pages (or run `python3 -m http.server` in this folder and open <http://localhost:8000>).

---

## Part 2 — Update your site in under 3 minutes

Everything happens in the browser, no software needed.

1. Go to your repo → click **`content.yml`** → click the **pencil ✏️ (Edit)** icon.
2. **Add a new entry.** Scroll to the `entries:` list near the bottom. Copy one of the templates (they're in the comments) and paste it as the newest item. Fill in the blanks. Example — a new paper:

   ```yaml
     - date: 2026-06-14
       type: publication
       title: "Your new article title"
       venue: "Journal Name, vol(issue), pages"
       links:
         - { text: "DOI", url: "https://doi.org/..." }
       tags: [CWD, surveillance]
   ```

3. Scroll down, click **Commit changes**. Your live site updates in ~1 minute.

**The four entry types** (the only values `type:` can take):

| `type:` | Appears on | Use for |
|---|---|---|
| `publication` | Publications (grouped by year) | papers, chapters, preprints, reports |
| `talk` | Outreach → Talks & presentations | conference talks, invited seminars |
| `outreach` | Outreach → Community engagement | workshops, public forums, partnerships |
| `fieldnote` | Photos & Field Notes | informal photo/notes (supports an `image:`) |

**Editing the slower stuff** (bio, courses, contact): just edit those blocks at the top of `content.yml` the same way.

**Three rules that prevent 99% of mistakes:**
- Indent with **2 spaces**, never tabs.
- If a value contains a colon `:`, wrap it in quotes → `title: "CWD: a 2026 update"`.
- A list item begins with `- `.

---

## Part 3 — The 5-week reminder system

**Important and by design:** a website is just static files — it has no way to send you reminders on its own. The reminder has to live in a system that *can* nudge you (a calendar, your email, or GitHub). You picked **Google Calendar**, which is the most reliable because it pings your phone and laptop. Here are your options, with the recommended one first.

### Recommended — Google Calendar (set up once, 2 minutes)

Easiest path: **import the included file.**
1. Open <https://calendar.google.com> on a computer.
2. Gear ⚙️ → **Settings → Import & export → Import**.
3. Choose `update-reminder.ics` from this folder, pick your calendar, click **Import**.
4. You now have a recurring all-day event **"Update academic website + CV"** every 5 weeks, with the full checklist in the notes. Adjust the start date if you like.

Prefer to make it by hand? Create an event titled *"Update website + CV (15 min)"*, set **Repeat → Custom → every 5 weeks**, add a notification, and paste the checklist from the `.ics` description into the notes.

### Alternative — GitHub Issue bot (lives with the site, free)

This repo includes an optional GitHub Action. Rename `.github/workflows/update-reminder.yml.optional` to `update-reminder.yml` and commit. Roughly every 5 weeks it opens a GitHub Issue with your checklist, and GitHub emails you. Good as a backup or if you'd rather keep everything in one place. (Cron timing is approximate, and GitHub may pause scheduled actions on inactive repos — fine as a secondary nudge.)

### Alternative — Email reminder (Gmail / Zapier / IFTTT)

In Gmail you can compose a reminder email to yourself and use **Schedule send**, then repeat it each cycle. For true automation, a free Zapier or IFTTT "Schedule → send email" zap every 5 weeks works without touching the site.

**Whichever you choose, the workflow is the same:** the reminder fires → you spend ~15 minutes adding entries to `content.yml` → commit → done.

---

## Part 4 — The ~15-minute refresh checklist

Keep this handy (it's also baked into the calendar reminder):

1. New publications / preprints accepted? → add a `publication` entry.
2. Talks or invited seminars given? → add a `talk` entry.
3. Outreach / community / Tribal partnership events? → add an `outreach` entry.
4. A field photo or short note worth sharing? → add a `fieldnote` entry.
5. Anything change in About / Teaching / Research? → edit those blocks.
6. CV changed? → re-upload `assets/Faust_CV.pdf`.
7. Commit. Live in ~1 minute.

---

## Part 5 — Optional upgrades for later

None of these are needed; the site is fully functional as-is. Add them when you have time.

- **ORCID integration** — simplest: link your ORCID in `profile.links` (already stubbed). For a live publication feed, ORCID offers a public API (`https://pub.orcid.org/v3.0/{your-id}/works`) you can fetch with a small JS snippet and render as entries. Keeping the manual list is often more reliable for review.
- **Google Scholar sync** — Scholar has no official API. Practical option: keep linking your profile (done). For automation, a periodic GitHub Action using a community scraper can refresh a citation count badge; treat it as best-effort.
- **CV auto-generation** — because all entries are structured data, a short script can read `content.yml` and emit a formatted CV (PDF via LaTeX/Pandoc, or a print-styled HTML page). This makes your website and CV a single source of truth. Ask and this can be added as a `cv.html` "print to PDF" page.
- **Blog / news feed** — you already have one: the Field Notes page plus the Home "Recent updates" feed. For longer posts, we can add a `type: post` with a body field.
- **Metrics / impact tracking** — add privacy-friendly analytics (e.g. Plausible or GoatCounter) with one script tag, or an Altmetric/Dimensions badge per publication.

---

## Troubleshooting

- **Page is blank or shows a load error online:** check that `content.yml` is in the same folder as `index.html` in the repo, and that `.nojekyll` was uploaded.
- **A YAML error after editing:** you almost certainly used a tab, or a value with a `:` that isn't quoted. Undo your last change (GitHub shows commit history) and reapply it carefully.
- **Image not showing:** confirm the file is in `assets/` and the path/case in `content.yml` matches exactly.
- **Want a different accent color:** open `index.html`, change `--accent` near the top of the `<style>` block. (The one thing in there worth touching.)
