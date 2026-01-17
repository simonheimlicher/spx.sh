# PRD: SPX Website

> **Purpose**: Defines the marketing and documentation website for the SPX Spec-Driven Development framework at spx.sh.

## Product Vision

### User Problem

**Who** are we building for?

Developers working with AI coding assistants (particularly Claude Code) who need structured workflows for managing specs, sessions, and development context across multiple projects.

**What** problem do they face?

```
As a developer using AI coding assistants, I am frustrated by the lack of discoverable documentation and marketing presence for SPX
because the CLI and Claude marketplace exist only as GitHub repos, which prevents me from understanding the value proposition and getting started quickly.
```

### Current Customer Pain

- **Symptom**: Developers must discover SPX through word-of-mouth or stumbling upon GitHub repos
- **Root Cause**: No dedicated website explains what SPX is, why it matters, or how to get started
- **Customer Impact**: Potential users cannot evaluate whether SPX solves their workflow problems
- **Business Impact**: Limited adoption and community growth for the SPX framework

### Customer Solution

```
Implement a marketing-focused documentation website that enables developers to understand SPX's value proposition
through clear messaging, installation guides, and conceptual documentation, resulting in increased adoption and community engagement.
```

### Customer Journey Context

- **Before**: Developers find spx-cli or spx-claude repos on GitHub with minimal README documentation; unclear value proposition
- **During**: Developers visit spx.sh, understand spec-driven development, follow installation guides, try the CLI
- **After**: Developers use SPX in their Claude Code workflows, contribute to the community, share with peers

### User Assumptions

| Assumption Category  | Specific Assumption                      | Impact on Product Design                                       |
| -------------------- | ---------------------------------------- | -------------------------------------------------------------- |
| Technical Capability | Comfortable with CLI tools and git       | Documentation can assume basic terminal proficiency            |
| Context              | May or may not already use Claude Code   | Must explain value for both new and existing Claude Code users |
| Goals                | Want structured, deterministic workflows | Emphasize speed, zero-token-cost, and reliability              |

## Expected Outcome

### Measurable Outcome

```
Developers will discover and adopt SPX leading to 100+ GitHub stars on spx-cli and spx-claude repos
and active community engagement, proven by GitHub metrics and issue/discussion activity within 6 months of launch.
```

### Evidence of Success

| Metric                    | Current | Target           | Improvement            |
| ------------------------- | ------- | ---------------- | ---------------------- |
| GitHub Stars (spx-cli)    | ~0      | 100+             | Community validation   |
| GitHub Stars (spx-claude) | ~0      | 100+             | Community validation   |
| Monthly Site Visitors     | 0       | 500+             | Discovery and interest |
| CLI Installations         | Unknown | 50+ active users | Adoption metric        |

## Acceptance Tests

### Complete User Journey Test

```typescript
describe("Feature: Developer discovers and adopts SPX", () => {
  test("developer understands value and installs CLI from landing page", async ({ page }) => {
    // Given: Developer visits spx.sh
    await page.goto("https://spx.sh/");

    // When: Developer explores the landing page
    await expect(page.locator("h1")).toContainText("SPX");
    await expect(page.locator("[data-testid='value-prop']")).toBeVisible();

    // And: Developer navigates to CLI documentation
    await page.click("[data-testid='nav-cli']");
    await expect(page).toHaveURL(/\/cli\//);

    // Then: Developer finds installation instructions
    await expect(page.locator("code")).toContainText("git clone");
    await expect(page.locator("[data-testid='install-commands']")).toBeVisible();
  });
});
```

### User Scenarios (Gherkin Format)

```gherkin
Feature: SPX Website Discovery and Adoption

  Scenario: New developer discovers SPX value proposition
    Given a developer visits spx.sh
    When they read the landing page content
    Then they understand what spec-driven development is
    And they see clear benefits (fast, deterministic, zero-token-cost)
    And they find links to get started

  Scenario: Claude Code user explores marketplace plugins
    Given a developer already uses Claude Code
    When they navigate to the Marketplace section
    Then they see available plugins (core, typescript, python, specs)
    And they find installation commands for their use case

  Scenario: Developer learns spec-driven development concepts
    Given a developer wants to understand the methodology
    When they navigate to the Concepts section
    Then they learn about spec hierarchy (capability/feature/story)
    And they understand status determination (DONE/IN PROGRESS/OPEN)
    And they understand BSP numbering for work items
```

## Scope Definition

### What's Included

- ✅ Marketing landing page with clear value proposition
- ✅ CLI documentation section (installation, commands, sessions)
- ✅ Marketplace documentation section (plugins, installation, creating plugins)
- ✅ Concepts section (spec-driven development methodology)
- ✅ About page with project information and links

### What's Explicitly Excluded

| Excluded Capability   | Rationale                                                                             |
| --------------------- | ------------------------------------------------------------------------------------- |
| Blog/News section     | Focus on core documentation first; blog adds maintenance burden                       |
| User accounts/login   | Static site simplicity; no user-specific features needed                              |
| Interactive tutorials | Complexity; defer until adoption validates demand                                     |
| Multi-language (i18n) | English-only simplifies maintenance; international audience can use translation tools |

### Scope Boundaries Rationale

This release focuses on establishing SPX's web presence with clear documentation. We're avoiding dynamic features (blogs, accounts, tutorials) until we validate that the core documentation drives adoption. A simple, fast static site maximizes developer trust and minimizes maintenance.

## Product Approach

### Interaction Model

- **Interface Type**: Static documentation website
- **Invocation Pattern**: Developer navigates to spx.sh via search, link, or direct URL
- **User Mental Model**: "Like a product landing page combined with technical docs"

### User Experience Principles

1. **Fast loading**: Sub-second page loads; no JavaScript-heavy frameworks
2. **Clear navigation**: Developer finds what they need in 2 clicks or less
3. **Copy-paste ready**: All code snippets are complete and work as shown
4. **Mobile responsive**: Readable on any device

### High-Level Technical Approach

**Content Structure:**

- Home page with marketing messaging and quick-start snippets
- Three main sections: CLI, Marketplace, Concepts
- Each section has landing page and sub-pages for detailed topics

**Technology Stack:**

- ⚠️ **ADR Trigger**: Static site generator choice (Hugo vs. alternatives)
- ⚠️ **ADR Trigger**: Deployment platform choice (Cloudflare Pages vs. alternatives)

**Design System:**

- Leverages existing hugo-claris theme from heimlicher.com
- Technical typography suitable for documentation
- Dark/light mode support

### Product-Specific Constraints

| Constraint                   | Impact on Product                         | Impact on Testing           |
| ---------------------------- | ----------------------------------------- | --------------------------- |
| Hugo static site generator   | Content in Markdown; builds must complete | Build verification in CI    |
| Cloudflare Pages hosting     | Deployment via GitHub Actions             | Preview deployments for PRs |
| hugo-claris theme dependency | Must work with theme conventions          | Theme compatibility testing |

## Success Criteria

### User Outcomes

| Outcome                         | Success Indicator                              |
| ------------------------------- | ---------------------------------------------- |
| Developers understand SPX value | Can explain SPX to a peer after visiting site  |
| Developers can install SPX      | Follow docs to working CLI in <5 minutes       |
| Developers find answers         | Navigate to relevant section without confusion |

### Quality Attributes

| Attribute         | Target                    | Measurement Approach               |
| ----------------- | ------------------------- | ---------------------------------- |
| **Performance**   | Lighthouse score >90      | Automated Lighthouse CI            |
| **Accessibility** | WCAG AA compliance        | Automated accessibility testing    |
| **SEO**           | Indexed by search engines | Google Search Console verification |
| **Uptime**        | 99.9% availability        | Cloudflare analytics               |

### Definition of "Done"

1. All three content sections (CLI, Marketplace, Concepts) have complete documentation
2. Site builds successfully with `npm run build`
3. Lighthouse performance score >90
4. Site deployed to spx.sh domain
5. GitHub repos linked and accessible

## Open Decisions

### Questions Requiring User Input

None identified - scope is clear from planning discussion.

### Decisions Triggering ADRs

| Decision Topic    | Key Question                        | Options to Evaluate                            | Triggers                                                               |
| ----------------- | ----------------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------- |
| Static site stack | Hugo + Cloudflare vs. alternatives? | Hugo/Cloudflare, Next.js/Vercel, Astro/Netlify | See [Hugo + Cloudflare ADR](decisions/adr-21_hugo-cloudflare-stack.md) |

### Product Trade-offs

| Trade-off              | Option A          | Option B       | Impact                                         |
| ---------------------- | ----------------- | -------------- | ---------------------------------------------- |
| Theme reuse vs. custom | Reuse hugo-claris | Custom theme   | A = faster launch, B = unique brand but delays |
| English only vs. i18n  | English only      | Multi-language | A = simpler, B = broader reach but maintenance |

## Dependencies

### Work Item Dependencies

| Dependency                   | Status   | Rationale                            |
| ---------------------------- | -------- | ------------------------------------ |
| spx-cli repository exists    | Complete | Source for CLI documentation         |
| spx-claude repository exists | Complete | Source for marketplace documentation |
| hugo-claris theme            | Complete | Provides layouts and styling         |

### Technical Dependencies

| Dependency       | Version/Constraint  | Purpose               | Availability      |
| ---------------- | ------------------- | --------------------- | ----------------- |
| Hugo             | >=0.153.0, <0.154.0 | Static site generator | Available via hvm |
| Node.js          | >=18.0.0            | Build tooling         | Assumed available |
| Cloudflare Pages | N/A                 | Hosting platform      | Available         |

### Performance Requirements

| Requirement Area    | Target      | Measurement Approach |
| ------------------- | ----------- | -------------------- |
| Page Load Time      | <1 second   | Lighthouse metrics   |
| Time to Interactive | <2 seconds  | Lighthouse metrics   |
| Build Time          | <30 seconds | CI timing            |

## Pre-Mortem Analysis

### Assumption: Developers will find the site through GitHub

- **Likelihood**: Medium - depends on README links and community sharing
- **Impact**: High - if not discoverable, no adoption
- **Mitigation**: Ensure prominent links from spx-cli and spx-claude READMEs; submit to relevant directories

### Assumption: hugo-claris theme works for documentation

- **Likelihood**: Low risk - already proven on heimlicher.com
- **Impact**: Medium - would require theme changes if inadequate
- **Mitigation**: Build early and verify all page types render correctly

### Assumption: Cloudflare Pages provides adequate performance

- **Likelihood**: Low risk - widely used for static sites
- **Impact**: Low - could migrate to alternative if needed
- **Mitigation**: Monitor with Lighthouse CI; Cloudflare has global CDN

### Assumption: Documentation scope is sufficient for adoption

- **Likelihood**: Medium - may discover gaps through user feedback
- **Impact**: Medium - may need additional content
- **Mitigation**: Track GitHub issues for documentation requests; iterate based on feedback
