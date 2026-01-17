# ADR: Hugo with Cloudflare Pages Deployment

## Problem

The SPX framework needs a documentation website at spx.sh. We need to choose a static site generator, theme/design system, and deployment platform that enables fast iteration, reliable hosting, and maintainable content.

## Context

- **Business**: SPX needs a professional web presence to drive adoption. The site must load fast, be easy to maintain, and cost-effectively scale.
- **Technical**: The maintainer (simonheimlicher) already operates heimlicher.com using Hugo + hugo-claris theme + Cloudflare Pages. Reusing this stack provides proven patterns and reduces learning curve.

## Decision

**Use Hugo with hugo-claris theme, deployed to Cloudflare Pages via GitHub Actions, mirroring the simonheimlicher/heimlicher.com architecture.**

## Rationale

Several static site generators were considered:

1. **Hugo** (chosen): Extremely fast builds (<3 seconds), Go-based single binary, mature ecosystem, already familiar to maintainer. The hugo-claris theme is battle-tested on heimlicher.com with professional typography, dark/light mode, and responsive design.

2. **Next.js/Astro**: Modern React/component-based approaches with good DX, but add JavaScript complexity for what is fundamentally a content site. Overkill for documentation.

3. **Jekyll**: Ruby-based, slower builds, requires Ruby environment. No advantage over Hugo.

4. **Docusaurus/VitePress**: Purpose-built for docs but opinionated structures. Hugo provides more flexibility while hugo-claris already has documentation-friendly layouts.

The deployment choice follows similar logic:

1. **Cloudflare Pages** (chosen): Free tier generous for static sites, global CDN, automatic HTTPS, GitHub integration, already used for heimlicher.com. GitHub Actions workflow exists and can be adapted.

2. **Vercel/Netlify**: Comparable features but would require new account setup and learning new deployment patterns.

3. **GitHub Pages**: More limited (no custom build commands, slower CDN).

Reusing the heimlicher.com stack provides:

- **Proven reliability**: Same configuration runs in production
- **Familiar patterns**: Maintainer knows the quirks and solutions
- **Shared improvements**: Theme updates benefit both sites
- **Faster launch**: No time spent learning new tools

## Trade-offs Accepted

- **Theme coupling**: Using hugo-claris ties SPX site styling to the theme's design decisions. Mitigation: Theme is actively maintained by same author; can fork if needed.
- **Hugo version sensitivity**: Hugo 0.154+ has breaking changes requiring version pinning. Mitigation: Using hvm (Hugo Version Manager) for reliable builds.
- **Go template learning curve**: Hugo's template syntax is unusual. Mitigation: Most content is Markdown; template changes rare after initial setup.

## Testing Strategy

### Level Coverage

| Level           | Question Answered                               | Scope                                 |
| --------------- | ----------------------------------------------- | ------------------------------------- |
| 1 (Unit)        | Does content render without errors?             | Markdown parsing, shortcodes          |
| 2 (Integration) | Does the full site build correctly?             | Hugo build process, asset pipeline    |
| 3 (E2E)         | Is the deployed site performant and accessible? | Lighthouse CI, live site verification |

### Escalation Rationale

- **1 → 2**: Individual page rendering doesn't verify cross-page navigation, asset bundling, or theme integration
- **2 → 3**: Local builds don't verify CDN performance, HTTPS configuration, or real-world load times

### Test Harness

| Level | Harness       | Location/Dependency                      |
| ----- | ------------- | ---------------------------------------- |
| 2     | Hugo build    | `npm run build:workspace`                |
| 3     | Lighthouse CI | `.github/workflows/cloudflare-pages.yml` |

### Behaviors Verified

**Level 1 (Unit):**

- Markdown files parse without Hugo errors
- Shortcodes (panel, lede-initial) render correctly
- Front matter is valid YAML

**Level 2 (Integration):**

- `npm run build:workspace` completes successfully
- All pages generate without warnings (or only expected warnings)
- Navigation links resolve correctly
- Assets (CSS, images, fonts) are bundled

**Level 3 (E2E):**

- Lighthouse performance score >90
- Lighthouse accessibility score >90
- Site loads in <1 second on broadband
- All pages accessible via navigation

## Validation

### How to Recognize Compliance

You're following this decision if:

- Site content is in `content/` as Markdown files
- Site builds with `npm run build:workspace` or `npm run dev`
- Deployment uses GitHub Actions to Cloudflare Pages
- Theme customizations go in `assets/sass/_custom.sass` or `_override.scss`

### MUST

- Use `npm run dev` or `npm run build:workspace` for all builds (loads env vars via dotenvx)
- Pin Hugo version via hvm to avoid 0.154+ breaking changes
- Keep theme as Go module dependency (not vendored copy)
- Configure Cloudflare Pages with same project structure as heimlicher.com

### NEVER

- Call `hugo` directly without npm scripts (missing env vars will break build)
- Upgrade Hugo past 0.153.x without testing theme compatibility
- Modify hugo-claris theme files directly (use override mechanisms instead)
- Deploy from local machine (always use GitHub Actions for consistency)
