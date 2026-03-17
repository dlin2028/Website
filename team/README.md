# Portfolio Build Team

A five-agent team to build Justin Leong's personal portfolio — a SvelteKit + Bun static site deployed to GitHub Pages.

## Agents

| Agent | File | Color | Responsibility |
|-------|------|-------|----------------|
| 🧭 Project Lead | [project-lead.md](project-lead.md) | Blue | Sprint planning, task sequencing, launch checklist |
| ✍️ Content Strategist | [content-strategist.md](content-strategist.md) | Green | Extract LinkedIn/resume → `src/lib/data.ts`, copy writing |
| 🎨 UI Designer | [ui-designer.md](ui-designer.md) | Purple | Design system, Tailwind config, component specs |
| 🔥 SvelteKit Developer | [sveltekit-developer.md](sveltekit-developer.md) | Orange | All routes, components, adapter-static build config |
| 🚀 DevOps Engineer | [devops-engineer.md](devops-engineer.md) | Red | GitHub Actions CI/CD pipeline, Pages deployment |

## Work Order

```
Content Strategist  →  data.ts + static assets
        ↓
UI Designer         →  app.css + Tailwind config + design specs
        ↓
SvelteKit Developer →  scaffold + all pages + components
        ↓
DevOps Engineer     →  .github/workflows/deploy.yml
        ↓
Project Lead        →  final checklist + launch sign-off
```

## Source Material

| File | Used By |
|------|---------|
| `Justin Leong _ LinkedIn.html` | Content Strategist |
| `Justin_s_Resume_3_17_25__Software_Focus_.pdf` | Content Strategist |
| `plan.md` | All agents — the spec |

## Key Outputs

| Path | Owner |
|------|-------|
| `src/lib/data.ts` | Content Strategist |
| `static/resume.pdf` | Content Strategist |
| `static/images/profile.jpg` | Content Strategist |
| `src/app.css` | UI Designer |
| `tailwind.config.ts` | UI Designer |
| `src/routes/**` | SvelteKit Developer |
| `.github/workflows/deploy.yml` | DevOps Engineer |
| `team/tasks.md` | Project Lead |
| `team/content-gaps.md` | Content Strategist |
| `team/repo-setup.md` | DevOps Engineer |
