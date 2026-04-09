# CLAUDE.md — JaguarAthleteCareerCards Site
## Jurupa Valley Jaguars Track & Field · Athlete Profile Hub

---

## What This Project Is

A static GitHub Pages website that hosts career performance data sheets for
Jurupa Valley High School (JVHS) track & field athletes. No frameworks, no
build step, no dependencies — pure HTML/CSS/JS files served directly by
GitHub Pages.

**Live URL:** `https://coachkevingarcia.github.io/JaguarAthleteCareerCards/`  
**Repo:** `https://github.com/CoachKevinGarcia/JaguarAthleteCareerCards`  
**Maintained by:** Coach Kevin Garcia  
**School colors:** Navy `#070e1c` · Silver `#b0c2dc` · White `#f0f5ff`  
**Accent:** Gold `#e8b84b`

---

## File Structure

```
JaguarAthleteCareerCards/
├── CLAUDE.md               ← You are here
├── index.html              ← Athlete roster / showcase index
├── logo.png                ← Jaguars T&F logo (shared by all pages)
├── ab-hernandez.html       ← A.B. Hernandez profile
├── nathaniel-oliver.html   ← Nathaniel Oliver profile
├── alexa-gomez.html        ← Alexa Gomez-Gonzalez profile
└── [athlete-name].html     ← Future athletes follow same pattern
```

**Rules:**
- All files live in the **root** of the repo. No subdirectories.
- File names are always `firstname-lastname.html` in lowercase with hyphens.
- `logo.png` is referenced as a relative path (`src="logo.png"`) on every page.

---

## Design System

All pages share the same CSS variable palette and font stack.
**Never deviate from these.** Copy them exactly into any new athlete page.

### Colors (CSS Variables)
```css
--navy:        #080f1e   /* page background */
--navy-mid:    #0e1b30   /* hero background */
--navy-card:   #111e34   /* card backgrounds */
--navy-border: #1a2d4a   /* all borders */
--silver:      #b8c8e0
--silver-light:#dce8f5
--white:       #f0f5ff
--gold:        #e8b84b   /* primary accent, PRs, wins */
--gold-dim:    rgba(232,184,75,0.15)
--accent:      #38beff   /* section titles, links, nav */
--accent-dim:  rgba(56,190,255,0.12)
--green:       #3de8a0   /* 1st place, wins */
--green-dim:   rgba(61,232,160,0.12)
--red:         #ff5e6b   /* injury markers */
--pr-col:      #ff5e6b   /* PR badges */
--muted:       #5a7299   /* labels, secondary text */
--injury:      #ff8c42   /* adversity/injury callouts */
```

### Fonts
```html
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Barlow+Condensed:wght@300;400;600;700&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
```
- **Bebas Neue** — athlete names, stat numbers, section headers
- **Barlow Condensed** — body text, table content, general UI
- **DM Mono** — section labels, mark values in tables, rankings

### Year Color Coding (consistent across all profiles)
| Grade | Color Variable | Chip Class |
|-------|---------------|------------|
| 9th   | `--green`     | `.y9`      |
| 10th  | `--accent`    | `.y10`     |
| 11th  | `--gold`      | `.y11`     |
| 12th  | `--red`       | `.y12`     |

### Place Badge Colors
| Place | Background    | Text       | Class |
|-------|--------------|------------|-------|
| 1st   | `--green`    | dark green | `.p1` |
| 2nd   | `--silver`   | navy       | `.p2` |
| 3rd   | `--gold`     | dark gold  | `.p3` |
| Other | dim white    | muted      | `.pn` |

---

## Page Architecture

### Every athlete page has these sections in order:

1. **`<nav class="site-nav">`** — Sticky top bar with ← All Athletes link + logo
2. **`.hero`** — Athlete name, school tag, event pills
3. **`.peak-bar`** — 3-column grid of career peak marks
4. **`.section` — Career Personal Bests** — `.bests-grid` of `.best-card` items
5. **`.section` — Career Milestones** — `.ms-grid` of `.ms-box` items
6. **`.section` — Event Logs** — `.log-table` for each event (TJ, LJ, HJ, Sprints, Hurdles)
7. **`.section` — Season Peaks** — `.peaks-stack` of `.peak-season` cards
8. **`.section` — Progression Chart** — SVG line chart
9. **`.section` — Rankings** (if applicable) — `.rank-grid`
10. **`.section` — Adversity`** (if applicable) — `.adversity-section` timeline
11. **`.section` — Coaching Notes** — `.notes-stack` of `.note-item` cards
12. **`<footer>`**

### Index page (`index.html`) structure:
1. **`.site-header`** — Logo + program title
2. **`.stats-strip`** — Scrollable program-level stats bar
3. **`.main`** — `.athlete-grid` of `.athlete-card` links
4. **`.about-section`** — Program description
5. **`<footer>`**

---

## How to Add a New Athlete

### Step 1 — Copy an existing profile
```bash
cp ab-hernandez.html firstname-lastname.html
```
Use AB's file as the template for girls jumps athletes.
Use nathaniel-oliver.html for boys hurdles/sprints athletes.

### Step 2 — Update the meta and title
```html
<title>First Last — Career Data Sheet</title>
```

### Step 3 — Update the hero section
```html
<div class="hero-school">Jurupa Valley Jaguars · [Boys/Girls] · [Events]</div>
<div class="hero-name">First<br><em>Last</em></div>
```
Pills — add one `.pill.gold` per primary event, `.pill` for secondary:
```html
<span class="pill gold">Triple Jump</span>
<span class="pill">Relays</span>
```

### Step 4 — Update peak bar (3 career bests)
```html
<div class="peak-val">42'2"</div>
<div class="peak-lbl">TJ Career PR</div>
```

### Step 5 — Fill in career bests cards
Each `.best-card` needs: event name, mark, meet context.
Left-border color class: `.gold`, `.blue`, or `.green`.

### Step 6 — Fill in log tables
Each row follows this exact pattern:
```html
<tr>
  <td><span class="yr-chip y9">9</span></td>
  <td class="mark-mono">36'0"</td>
  <td><span class="place-dot p1">1</span></td>
  <td class="meet-txt">Meet Name Here</td>
</tr>
```
For PR marks add class `pr` to `.mark-mono` and append ` ★`:
```html
<td class="mark-mono pr">42'2.75" ★</td>
```
For injury/DNS rows:
```html
<td class="mark-mono" style="color:var(--muted)">DNS</td>
<td class="meet-txt" style="color:var(--injury)">Raincross ⚠️ injury</td>
```

### Step 7 — Update season peaks
One `.peak-season` block per year competed. Add injury note if applicable:
```html
<div class="injury-note">⚠️ Brief description of injury / missed meets</div>
```

### Step 8 — Update SVG chart
The chart uses a simple linear scale. Adjust `viewBox` values and plot points
based on the athlete's actual progression range. See existing charts as
reference — the key values to change are the `points` in `<polyline>` and
`<polygon>`, and the `cy` values of `<circle>` elements.

### Step 9 — Update coaching notes
Write honest, data-driven assessments. Each `.note-item` covers one event
or theme. Use border color classes `.gold`, `.blue`, `.green`, `.orange`.

### Step 10 — Add the athlete to index.html
Find the `.athlete-grid` div and add a new `.athlete-card`:
```html
<a href="firstname-lastname.html" class="athlete-card">
  <div class="card-accent-bar bar-gold"></div>  <!-- bar-gold / bar-blue / bar-green -->
  <div class="card-body">
    <div class="card-yr">[Grade] · [Boys/Girls] · [Events]</div>
    <div class="card-name">First <span class="card-name-last">Last</span></div>
    <div class="card-events">
      <span class="event-tag hl">Primary Event</span>
      <span class="event-tag">Secondary Event</span>
    </div>
    <div class="card-divider"></div>
    <div class="card-peaks">
      <div class="peak-cell">
        <div class="peak-mark">42'2"</div>
        <div class="peak-event">Triple Jump PR</div>
      </div>
      <!-- 3 peak cells total -->
    </div>
  </div>
  <div class="card-footer">
    <div class="card-rankings">Event: <strong>Ranking Info</strong></div>
    <div class="card-cta">Full Profile</div>
  </div>
</a>
```
Also update the `.stats-strip` numbers at the top of `index.html` if needed
(athlete count, River Valley #1 rankings count, etc.).

---

## How to Update an Existing Athlete's Marks

### After a meet — typical workflow:

1. Open the athlete's `.html` file
2. Find the correct log table (TJ, LJ, HJ, etc.)
3. Add a new `<tr>` row at the bottom of that season's block
4. If the new mark is a PR:
   - Add `pr` class to `.mark-mono` and append ` ★`
   - Update the career best in the `.bests-grid` section
   - Update the `.peak-bar` at the top if it's an overall career best
5. If it's a season best, update the `.peak-season` card for the current year
6. Update the SVG chart endpoint if the season best changed
7. If rankings changed, update the `.rank-grid` section

### Quick reference — what to update for a new PR:
- [ ] Log table row (new `<tr>`)
- [ ] `.best-card` for that event
- [ ] `.peak-bar` career stat (top of page)
- [ ] `.peak-season` current year card
- [ ] SVG chart (if season best changed)
- [ ] Rankings grid (if rankings changed)
- [ ] Index card `.peak-mark` (if it's in the top 3 marks shown)

---

## Adversity Section (Optional)

Only include this section if the athlete has a meaningful injury/comeback
story worth documenting. Use the `.adversity-section` component:

```html
<div class="adversity-section">
  <div class="adv-header">
    <div class="adv-icon">🦅</div>
    <div>
      <div class="adv-title">Section Title</div>
      <div class="adv-sub">brief subtitle</div>
    </div>
  </div>
  <div class="adv-timeline">
    <div class="adv-item injury">   <!-- injury / triumph / comeback -->
      <div class="adv-line"></div>
      <div>
        <div class="adv-yr-tag">GRADE — EVENT LABEL</div>
        <div class="adv-text">Narrative text here.</div>
        <div class="adv-result">⚠️ Result or outcome</div>
      </div>
    </div>
  </div>
</div>
```
Item modifier classes: `injury` (orange), `triumph` (gold), `comeback` (green).

---

## Mobile Optimization Rules

All pages are built mobile-first for Galaxy S25 Ultra and iPhone 17.
Always follow these rules:

- `max-width: 540px` on `body` with `margin: 0 auto`
- Use `env(safe-area-inset-top)` and `env(safe-area-inset-bottom)` for padding
- Sticky nav uses `backdrop-filter: blur(10px)` for legibility while scrolling
- Tables use `font-size: 12px` — do not go smaller
- Touch targets minimum `44px` tall
- No horizontal scroll — test every table on a 375px viewport
- `-webkit-tap-highlight-color: transparent` on `*`
- `-webkit-font-smoothing: antialiased` on `body`

---

## Deployment

This is a pure static site. No build process. No npm. No config.

```bash
# Make a change, then:
git add .
git commit -m "Update AB Hernandez — new TJ mark 41'5\" at League Finals"
git push origin main
```

GitHub Pages auto-deploys on every push to `main`. Changes are live within
~30 seconds at `https://coachkevingarcia.github.io/JaguarAthleteCareerCards/`.

---

## Git Commit Message Convention

Keep commit messages specific so the history reads like a meet log:

```
# Good:
Update Nathaniel Oliver — 110mH PR 16.31 at RVL Championships, 1st place
Add Donyell Stephens profile — sprints, 9th-12th career
Update index stats strip — 4 athletes, 9 River Valley #1 rankings
Fix: Alexa Gomez LJ log missing Arcadia meet entry

# Bad:
update site
fix stuff
add athlete
```

---

## Current Athletes

| File | Athlete | Grade | Events | Notable |
|------|---------|-------|--------|---------|
| `ab-hernandez.html` | A.B. Hernandez | 12th (Girls) | TJ, LJ, HJ | CIF State TJ Champion '25, CA #2 TJ |
| `nathaniel-oliver.html` | Nathaniel Oliver | 12th (Boys) | 110mH, 300mH, HJ | RV #1 all hurdles + HJ, overcame 3 injuries |
| `alexa-gomez.html` | Alexa Gomez-Gonzalez | 11th (Girls) | TJ, LJ, 100mH, Sprints | Multi-event, PR in every event '25 season |

---

## Data Sources

All marks come from official meet results (MileSplit / athletic.net).
When adding marks, always record:
- Final mark (feet/inches for jumps, seconds for track)
- Wind reading if applicable e.g. `(1.3)`
- Place finish
- Meet name
- Date

Wind-assisted marks (> 2.0 m/s) should be noted but still recorded.
Marks labeled `c` (converted/hand-timed) should keep the `c` suffix.
PR and SB should be marked in the data — PR takes priority over SB.

---

## Coach Notes on Style

- **Tone:** Direct, data-driven, honest. These sheets are for athletes and
  coaches — not social media. Avoid hype language.
- **PRs:** Always mark with ★ in tables and `pr-tag` badge in bests cards.
- **Injuries:** Document them. They are part of the story and matter for
  context when evaluating performance gaps.
- **Coaching notes:** Write what you would say to the athlete or a college
  recruiter. What's the ceiling? What's developing? What's the pattern?
- **Rankings:** Only include rankings that are current-season and verified
  from MileSplit or athletic.net. Don't estimate.
