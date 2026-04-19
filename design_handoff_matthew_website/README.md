# Handoff: Matthew Rhodes Personal Website

## Overview
A personal portfolio website for Matthew Rhodes — AI Agent Engineer & Data Scientist. The site consists of four pages: Home, About, Blogs, and Resume, plus an external GitHub link. The design language is two-toned: the **Home page** uses a dark cinematic feel (deep blue-black with a fullscreen background video), while the **inner pages** (About, Blogs, Resume) share an **Ancient Greek + lush greenery** aesthetic — deep forest green backgrounds, marble-cream typography, gold ornamental accents, and Cormorant Garant serif display type.

## About the Design Files
The files in this bundle are **design references created in HTML** — high-fidelity prototypes showing the intended look, content, and interactive behavior. They are **not** production code to ship directly. The task is to **recreate these designs in the target codebase's environment** (e.g. React, Next.js, Vue, etc.) using its established patterns, routing, and component libraries. If no environment exists yet, Next.js (App Router) with Tailwind CSS is a good fit for this project.

## Fidelity
**High-fidelity.** These are pixel-close mockups with final colors, typography, spacing, copy, and interactions. Recreate them as closely as possible in the target framework, applying the codebase's conventions for routing, styling, and component structure.

---

## Design Tokens

### Colors
| Token | Value | Usage |
|---|---|---|
| `--bg` | `#0d1f0d` | Inner page background |
| `--bg2` | `#111f11` | Secondary background |
| `--surface` | `rgba(205,195,165,0.07)` | Card hover, subtle fills |
| `--surface2` | `rgba(205,195,165,0.12)` | Skill tags, raised surfaces |
| `--gold` | `#c8a84b` | Accents, active nav, dates, tags |
| `--gold-dim` | `rgba(200,168,75,0.3)` | Portrait overlay |
| `--cream` | `#ece4cc` | Primary text |
| `--sage` | `#7a9e7e` | Secondary headings, org names |
| `--sage-dim` | `rgba(122,158,126,0.25)` | Portrait overlay |
| `--muted` | `#6a8a6e` | Body text, nav links |
| `--border` | `rgba(200,168,75,0.2)` | All borders and dividers |
| Home `--background` | `hsl(201,100%,13%)` | Hero page bg (deep navy) |
| Home `--muted-foreground` | `hsl(240,4%,66%)` | Hero subtitle / muted text |

### Typography
| Role | Font | Size | Weight | Notes |
|---|---|---|---|---|
| Display headings | Cormorant Garant | clamp(3rem–4.5rem) | 400 | Italic variant for accent words |
| Logo (home) | Instrument Serif | 1.875rem | 400 | Letter-spacing -0.03em |
| Logo (inner) | Cormorant Garant | 1.7rem | 400 | |
| Nav links | Inter | 0.82rem | 400 | Uppercase, letter-spacing 0.12em |
| Body / bullets | Inter | 0.875–1.05rem | 300 | Line-height 1.75–1.85 |
| Eyebrows / labels | Inter | 0.65–0.72rem | 400 | Uppercase, letter-spacing 0.18–0.2em, gold color |
| Skill tags | Inter | 0.7rem | 400 | |
| Stats number | Cormorant Garant | 3rem | 400 | Gold color |

### Spacing & Shape
- Max content width: **1100px** (inner pages), **1280px** (home hero)
- Page horizontal padding: **40px** desktop, **24px** mobile
- Card gap: **2px** (grid background = border color, creates hairline dividers)
- Border radius: **2px** (almost square — intentional)
- Greek Key top border: 4px repeating gold pattern, opacity 0.45

---

## Pages & Screens

### 1. Home (`index.html`)
**Purpose:** Hero landing page with fullscreen background video and intro video modal.

**Layout:**
- Full-viewport, dark (`hsl(201,100%,13%)`)
- Fixed `<video>` element behind everything (`position: fixed; inset: 0; object-fit: cover; z-index: 0`)
- Nav bar: flex row, space-between, max-width 1280px, padding 24px 32px
- Hero: centered column, `min-height: 100vh`, text-align center, padding 90px 24px

**Nav components:**
- Logo: "Matthew" — Instrument Serif 1.875rem
- Nav links: hidden on mobile, flex gap-32px on ≥768px. Colors: muted by default, white on hover/active
- CTA button "Intro Video": pill shape (border-radius 9999px), liquid glass effect (see below), opens intro modal

**Hero components:**
- `<h1>`: "Agent Engineer & Data Scientist" — Instrument Serif, clamp(3rem–6rem), letter-spacing -0.061em
- CTA button "Intro Video": same liquid glass pill, opens intro modal

**Liquid Glass Effect:**
```css
background: rgba(255,255,255,0.01);
backdrop-filter: blur(4px);
box-shadow: inset 0 1px 1px rgba(255,255,255,0.1);
/* ::before pseudo — gradient border top+bottom */
padding: 1.4px gradient border using -webkit-mask xor technique
```

**Animations:** `fade-rise` keyframe (opacity 0→1, translateY 24px→0) over 0.8s, staggered 0s / 0.2s / 0.4s delays.

**Video Setup:**
- Background video: `<video id="video-bg" autoplay muted loop playsinline>`
  - Add `<source src="videos/background.mp4" type="video/mp4">` ← **file to be provided**
- Intro modal video: `<video id="intro-video" controls playsinline>`
  - Add `<source src="videos/intro.mp4" type="video/mp4">` ← **file to be provided**

**Intro Video Modal:**
- Triggered by clicking either "Intro Video" button (class `.intro-video-btn`)
- Full-viewport overlay: `background: rgba(0,0,0,0.85)`, `backdrop-filter: blur(8px)`
- Inner container: `90vw`, `max-width: 960px`, `aspect-ratio: 16/9`
- Opens with opacity + scale transition (0.95 → 1.0 over 0.3s)
- Closes on: ✕ button, backdrop click, Escape key
- On close: pause video + reset `currentTime = 0`

---

### 2. About (`about.html`)
**Purpose:** Bio, portrait, and mission statement.

**Layout:**
- Sticky nav (same structure as inner pages — see Shared Nav below)
- Greek key border strip at top (4px)
- Hero section: 2-column grid (`280px 1fr` → stacks on mobile), gap 80px, padding 100px 40px 80px
- Mission section: full-width grid of 4 cards (2×2), gap 2px

**Left column:**
- Eyebrow: "Agent Engineer & Data Scientist" — gold, uppercase, 0.72rem
- `<h1>`: "Building *solutions* that *matter*" — Cormorant Garant, clamp 3–4.5rem, italic words in `--sage`
- Two bio paragraphs — Inter 1.05rem, 300 weight, 0.75 opacity cream
- Stats row: "5+" / "∞" — Cormorant Garant 3rem gold; labels uppercase 0.78rem muted

**Right column (portrait):**
- `aspect-ratio: 4/5`, border 1px gold-border, border-radius 2px
- `<img src="assets/IMG_2103.JPG">` — `object-fit: cover; object-position: top center`
- Gradient overlay: `linear-gradient(135deg, sage-dim, transparent)` + `linear-gradient(315deg, gold-dim, transparent)`
- Inner inset border: absolute pseudo-element 12px inset

**Mission cards (4-up grid):**
- Background: `--bg`, on hover: `--surface`
- Padding 40px, transition background 0.3s
- Each card: emoji icon (1.8rem), `<h3>` Cormorant Garant 1.4rem, `<p>` Inter 0.9rem muted
- Topics: Empower Minorities, Help the Homeless, Reduce Pollution, Improve Healthcare

---

### 3. Blogs (`blogs.html`)
**Purpose:** Grid of 3 blog post cards linking to external AWS blog posts.

**Layout:**
- Page header: max-width 1100px, padding 80px 40px 60px, border-bottom gold
- Card grid: `repeat(auto-fill, minmax(320px, 1fr))`, gap 2px, background = border color (hairline effect)

**Card structure:**
- `<a>` tag — entire card is a link, `target="_blank"`
- Padding 40px, background `--bg`, hover → `--surface`
- Tag (eyebrow, gold), Title (Cormorant Garant 1.5rem), Excerpt (Inter 0.875rem muted), Footer with date + ↗ arrow
- Arrow animates: `transform: translate(4px, -4px)` on card hover

**Blog posts & URLs:**
| Title | URL |
|---|---|
| Small Anomaly Detection | https://aws.amazon.com/blogs/machine-learning/detect-defects-in-automotive-parts-with-amazon-lookout-for-vision-and-amazon-sagemaker/ |
| Using Graph Neural Networks to Generate Movie Recommendations | https://aws.amazon.com/blogs/machine-learning/part-2-power-recommendations-and-search-using-an-imdb-knowledge-graph/ |
| Building a Career Recommendation Engine | https://aws.amazon.com/blogs/machine-learning/how-rallypoint-and-aws-are-personalizing-job-recommendations-to-help-military-veterans-and-service-providers-transition-back-into-civilian-life-using-amazon-personalize/ |

---

### 4. Resume (`resume.html`)
**Purpose:** Full resume displayed inline with a PDF download button.

**Layout:**
- Page header: flex row space-between, Download PDF button (gold, border-radius 2px)
- Body: 2-column grid (`260px 1fr`), gap 60px → stacks on mobile

**Sidebar:**
- Contact: email (matthewdatarhodes@gmail.com), GitHub (MatthewCodes), Location (Mountain View, CA)
- Skills grouped: Expert (Python, LLMs, ML, Deep Learning, Langgraph, Git), Experienced (SQL, JS, AWS, Bedrock, RAG), Tools (Eleven Labs, Deepgram, LiveKit, ReTool)
- Education: MS Data Science UW 2019–2021; BS CS + Minor Entrepreneurship MSU 2015–2019

**Main content — Work Experience:**
1. AI Agent Engineer — Liberate Inc., Berkeley (May 2025 – Apr 2026)
2. Data Scientist II — Amazon GenAI Innovation Center, Santa Clara (Feb 2023 – May 2025)
3. Data Scientist I — Amazon ML Solutions Lab, Santa Clara (Apr 2021 – Feb 2023)
4. CEO — Mortodoo Inc., Detroit (Jan 2022 – Present)

**Main content — Publications:**
1. Zero-shot Hierarchical NER with LLMs — Amazon ML Conference, Sep–Nov 2023
2. Scalable Generative Data Augmentation: Medical-Grade Images — Amazon ML Conference, Aug 2023–Oct 2024

**Entry layout:** CSS grid `1fr auto` — title + date on same row, org full-width below, bullet list full-width below that.

**Download button:** links to `assets/Matthew_Rhodes_AI_Agent_Engineer-2.pdf` — download attribute triggers PDF save.

---

## Shared Nav (inner pages)
- `position: sticky; top: 0; z-index: 100`
- Background: `rgba(13,31,13,0.88)`, `backdrop-filter: blur(12px)`
- Border-bottom: 1px gold border
- Logo: "Matthew" — Cormorant Garant 1.7rem, links to `index.html`
- Links (left to right): Home, Blogs, About, Github (→ https://github.com/MatthewCodes, target blank), Resume
- Active link: gold color
- Right CTA: "Intro Video" — gold background, dark text, uppercase, 0.8rem, border-radius 2px, links to `index.html` (or triggers modal)

---

## Interactions & Behavior
- All inner page nav links have active state (gold color) matching current page
- Blog cards: entire card is clickable, opens in new tab
- Resume download: browser native download of PDF
- Home intro modal: see detailed spec under Home page above
- Entrance animations: `fade-up` (opacity 0→1, translateY 20px→0, 0.7s ease-out) staggered with `.anim-1` through `.anim-4` (0.1s–0.4s delays)

---

## Assets
| File | Usage |
|---|---|
| `assets/IMG_2103.JPG` | Portrait photo on About page |
| `assets/Matthew_Rhodes_AI_Agent_Engineer-2.pdf` | Resume PDF download |
| `videos/background.mp4` | **To be provided** — fullscreen home page bg video |
| `videos/intro.mp4` | **To be provided** — intro video modal on home page |

---

## Files in This Bundle
| File | Description |
|---|---|
| `index.html` | Home page — hero + video bg + intro modal |
| `about.html` | About page |
| `blogs.html` | Blogs listing page |
| `resume.html` | Resume page |
| `greek-shared.css` | Shared CSS for inner pages (nav, tokens, animations, ornaments) |
| `assets/IMG_2103.JPG` | Portrait photo |
| `assets/Matthew_Rhodes_AI_Agent_Engineer-2.pdf` | Resume PDF |
