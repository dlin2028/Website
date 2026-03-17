# Personal Portfolio Website — Build Plan

## Source Material
| File | Purpose |
|------|---------|
| `Justin Leong _ LinkedIn.html` | Profile content: headline, experience, education, skills |
| `Justin_s_Resume_3_17_25__Software_Focus_.pdf` | Resume content for the downloadable resume and Projects/Experience sections |

---

## Tech Stack
| Layer | Choice | Reason |
|-------|--------|--------|
| Framework | **SvelteKit** | File-based routing, zero-JS by default, great DX |
| Runtime / Package manager | **Bun** | Fast installs, built-in bundler, can run `vite` via Bun |
| Static output | `@sveltejs/adapter-static` | Generates a `build/` folder of plain HTML/CSS/JS |
| Styling | **Tailwind CSS v4** | Utility-first, works cleanly with SvelteKit |
| Fonts / Icons | Google Fonts + Lucide (or Heroicons) | Lightweight, self-hostable copies for offline |

---

## Project Structure
```
portfolio/
├── bun.lock
├── package.json
├── svelte.config.js          # adapter-static config
├── vite.config.ts
├── tailwind.config.ts
├── static/
│   ├── favicon.ico
│   ├── resume.pdf            # copy of Justin_s_Resume_...pdf
│   └── images/
│       └── profile.jpg
└── src/
    ├── app.html
    ├── app.css               # Tailwind base + custom vars
    └── routes/
        ├── +layout.svelte    # Nav + footer shell
        ├── +page.svelte      # Hero / landing
        ├── about/
        │   └── +page.svelte
        ├── experience/
        │   └── +page.svelte
        ├── projects/
        │   └── +page.svelte
        └── contact/
            └── +page.svelte
```

---

## Pages & Content

### `/` — Hero
- Name: **Justin Leong**
- Headline: *Software Developer | Machine Learning (PyTorch, TensorFlow) | Exploring AI & Deep Learning*
- Location: San Ramon, CA
- CTAs: [View Resume] → `static/resume.pdf`  |  [Contact Me] → `/contact`
- Subtle animated background or gradient

### `/about`
- Short bio sourced from LinkedIn "About" section
- Education:
  - M.S. — University of California, Irvine (in progress)
  - B.S. — [source from resume]
- Open-to-work badge (roles: Software Engineer, Computer Engineer, AI Engineer)

### `/experience`
- Timeline or card layout
- **Advantest** — Software Engineer / Developer
  - Dates & bullet points from LinkedIn / resume
- Additional roles as listed on resume

### `/projects`
- Cards with title, tech stack badges, short description, optional GitHub link
- Source project names and descriptions from resume

### `/contact`
- LinkedIn link → `https://www.linkedin.com/in/justinleong` (verify exact slug)
- Email (from resume)
- GitHub link (from resume)
- Simple form (static-site-friendly: use Formspree or Netlify Forms)

---

## Setup Steps

```bash
# 1. Scaffold SvelteKit project with Bun
bunx sv create portfolio
# choose: SvelteKit minimal, TypeScript yes, Tailwind yes

cd portfolio

# 2. Install static adapter
bun add -D @sveltejs/adapter-static

# 3. Configure svelte.config.js
# import adapter from '@sveltejs/adapter-static';
# export default { kit: { adapter: adapter({ pages: 'build', assets: 'build', fallback: undefined }) } };

# 4. Dev server
bun run dev

# 5. Build static output
bun run build
# output: build/
```

---

## Data Strategy
1. **Extract resume text** — run `pdftotext resume.pdf` (or install `pypdf` once available) to get plain text, then manually split into structured data.
2. **Structured content file** — store all profile data in `src/lib/data.ts` as typed objects (experience array, projects array, skills list) so pages stay clean.
3. **Images** — copy profile photo from `Justin Leong _ LinkedIn_files/` into `static/images/`.

---

## Deployment — GitHub Pages

**Primary target: GitHub Pages** via GitHub Actions.

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/checkout@v4
      - uses: oven-sh/setup-bun@v2
        with: { bun-version: latest }
      - run: bun install
      - run: bun run build
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with: { path: build }
      - id: deployment
        uses: actions/deploy-pages@v4
```

Enable **GitHub Pages → Source: GitHub Actions** in repo settings.  
Set `paths.base` in `svelte.config.js` to `'/repo-name'` if deploying to a project page (not a user `*.github.io` root page).

---

## Nice-to-Haves (post-MVP)
- Dark / light mode toggle (CSS custom properties + Svelte store)
- Subtle scroll animations (Intersection Observer, no extra lib needed)
- OG meta tags for social sharing
- Lighthouse score target: 100/100 Performance, 100 Accessibility
