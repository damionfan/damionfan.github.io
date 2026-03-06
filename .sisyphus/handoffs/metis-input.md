# Agent Input: Metis

## Task
Review the GitHub Pages academic homepage project at `/home/shengyu/damionfan.github.io` (deployed at `https://damionfan.github.io`). Analyze the codebase for issues, gaps, and provide optimization recommendations. This is an **academicpages** Jekyll template used by a PhD student.

## Context (Explore Findings)

### Project Overview
- Jekyll-based academic homepage using **academicpages** template
- Owner: **Shengyu Fan (范胜玉)**, PhD candidate at IIE/Chinese Academy of Sciences
- Research: FHE accelerators, LLM accelerator/system design
- URL: https://damionfan.github.io
- Repository: damionfan/damionfan.github.io

### Critical Issues Found by Explore

1. **Navigation completely disabled**: ALL navigation links in `_data/navigation.yml` are commented out — the site has no top nav menu at all
2. **CV page is 100% template placeholder**: `_pages/cv.md` still says "GitHub University", "Skill 1", "Professor Git" — never customized
3. **Publications page outdated**: `_pages/publications.md` is missing all 2025 papers (MICRO'25, ISCA'25×2, HPCA'25, CCS'25) and ASPLOS'26, HPCA'26 that ARE on the about.md homepage
4. **Duplicate publications**: Publications appear both in `about.md` (homepage) and `_pages/publications.md` — with different formatting and different content
5. **Profile image unoptimized**: `images/profile.jpg` is 610KB — very large for a headshot
6. **Timezone wrong**: `_config.yml` has `timezone: America/Los_Angeles` — should be `Asia/Shanghai`
7. **Only 1 placeholder blog post**: `_posts/2012-08-14-blog-post-1.md` — template demo content
8. **Template demo content in collections**: `_talks/`, `_teaching/`, `_portfolio/` still contain template example entries
9. **SEO not configured**: `google_site_verification`, `bing_site_verification` etc. all empty
10. **Analytics tracking ID empty**: `analytics.provider` set to `google-universal` but no `tracking_id`
11. **Typo in about.md**: "finial year" should be "final year"
12. **Grammar issues**: "Two paper are accepted" should be "Two papers are accepted", "One paper are accepted" should be "One paper is accepted"
13. **Many paper links point to "TBD"**: Several recent publications have `(TBD)` instead of actual URLs
14. **`sitemap: false`** on about.md and publications.md — these key pages are excluded from sitemap
15. **Google verification file exists** (`google2301496222d4dbe0.html`) but site verification not set in config

### Key Files
- `_config.yml` — main configuration (337 lines)
- `_pages/about.md` — homepage (103 lines)
- `_pages/publications.md` — publications page (46 lines)
- `_pages/cv.md` — CV page (65 lines, all placeholder)
- `_data/navigation.yml` — navigation (26 lines, all commented out)
- `images/profile.jpg` — profile photo (610KB)

## Output Location
`.sisyphus/handoffs/metis-report.md`

## Completion Signal
Write `<!-- AGENT_COMPLETE -->` as the last line of your output file when done.

---

## Agent Instructions

You are Metis, the Pre-Planning Analyst. Your job is to:

1. **Classify the intent**: This is a REVIEW + OPTIMIZATION task (Research/Mid-sized hybrid)
2. **Deep-dive into issues**: Read key files yourself to verify and expand on the Explore findings above
3. **Prioritize findings**: Categorize as Critical / Important / Nice-to-have
4. **Surface questions**: If scope is unclear, write specific questions for the user
5. **Write directives for Prometheus**: What the plan MUST and MUST NOT include

### Key areas to investigate:
- Content completeness and accuracy
- SEO and discoverability
- Performance (image sizes, asset loading)
- Mobile-friendliness
- Template cleanup (remove demo content)
- Academic best practices (publications formatting, Google Scholar, ORCID)
- Configuration correctness

### CONSTRAINTS
- **READ-ONLY**: Do NOT modify any project files
- Write your report to `.sisyphus/handoffs/metis-report.md`
- End with `<!-- AGENT_COMPLETE -->`
