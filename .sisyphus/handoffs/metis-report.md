# Metis Report: GitHub Pages Academic Homepage Review

## Intent Classification
- **Type**: Research / Mid-sized Hybrid (Review + Optimization recommendations)
- **Confidence**: High
- **Complexity**: Complex (15+ distinct issues across content, config, SEO, performance, and template cleanup)
- **Rationale**: User requests comprehensive review and optimization. Multiple files need changes across different categories. This is a deployed academic homepage that represents the user professionally.

## Pre-Analysis Findings

### 🔴 Critical Issues (Directly harms professional image)

1. **Navigation completely disabled** (`_data/navigation.yml:1-26`)
   - ALL navigation links are commented out
   - Visitors can only see the homepage — no way to navigate to publications, CV, talks, etc.
   - This makes the site effectively a single-page with no discoverability

2. **CV page is 100% template placeholder** (`_pages/cv.md:12-65`)
   - Education: "Ph.D in Version Control Theory, GitHub University, 2018"
   - Work: "Academic Pages Collaborator", "Professor Hub", "Professor Git"
   - Skills: "Skill 1", "Skill 2", "Sub-skill 2.1"
   - A visitor clicking CV sees fake data — severely damages credibility

3. **Publications page outdated and inconsistent** (`_pages/publications.md`)
   - Missing all 2025 papers: MICRO'25 (HAWK), ISCA'25 ×2 (FAST, Neo), HPCA'25 (WarpDrive), CCS'25
   - Missing 2026 papers: ASPLOS'26, HPCA'26 (mentioned in News but no listings)
   - Different formatting from about.md (uses `<span>` tags vs shields.io badges)
   - Typo: "MCIRO2024" should be "MICRO2024"
   - `_publications/` collection directory doesn't exist — CV page loop is empty

4. **Timezone misconfigured** (`_config.yml:283`)
   - Set to `America/Los_Angeles` — user is in Beijing, China
   - Should be `Asia/Shanghai`

### 🟡 Important Issues (Affects quality and SEO)

5. **Homepage excluded from sitemap** (`_pages/about.md:8`)
   - `sitemap: false` on the homepage/about page — Google won't index it properly
   - Same issue on publications page

6. **Profile image unoptimized** (`images/profile.jpg` = 610KB)
   - A headshot should be ~50-100KB max
   - Slows page load significantly, especially on mobile

7. **Typos and grammar errors** (`_pages/about.md`)
   - Line 22: "finial year" → "final year"
   - Line 41: "One paper are accepted" → "One paper is accepted"
   - Line 42: "Two paper are accepted" → "Two papers are accepted"
   - Line 47: "Two paper are accepted" → "Two papers are accepted"

8. **Multiple paper links are "TBD"** (`_pages/about.md:55-67`)
   - HAWK (MICRO'25), FAST (ISCA'25), Neo (ISCA'25), WarpDrive (HPCA'25) all link to "(TBD)"

9. **Analytics misconfigured** (`_config.yml:139-141`)
   - Provider set to `google-universal` but `tracking_id` is empty
   - Either add tracking ID or remove the provider setting

10. **Google site verification inconsistent** (`_config.yml:115`)
    - `google2301496222d4dbe0.html` exists in root but `google_site_verification` config is empty

### 🟢 Nice-to-have Improvements

11. **Template demo content remains**
    - `_talks/`: 4 placeholder talk entries from 2012-2014
    - `_teaching/`: 2 placeholder teaching entries
    - `_portfolio/`: 2 placeholder portfolio entries
    - `_posts/`: 1 placeholder blog post from 2012
    - `_drafts/`: 1 placeholder draft
    - `_data/authors.yml`: Template placeholder authors

12. **Missing academic profile links** (`_config.yml:34-38`)
    - ORCID not configured (commented out)
    - arXiv profile not linked
    - ResearchGate not linked

13. **`_pages/` cleanup needed**
    - `markdown.md` (markdown guide demo page) still present
    - `archive-layout-with-content.md` (template demo) still present
    - `terms.md` (template terms page) still present
    - `non-menu-page.md` (template demo) still present

14. **No favicon customized** — using template default (`images/favicon.ico`)

15. **`_publications/` collection missing**
    - `_config.yml` defines a `publications` collection but the `_publications/` directory doesn't exist
    - CV page tries to iterate over this empty collection

## Test Infrastructure
- **Present**: NO (static Jekyll site — no test framework)
- **Framework**: N/A
- **Decision**: Verification via Jekyll build + visual inspection

## Questions for User

### Q1: Which pages should be enabled in the navigation?
**Options:**
- A) All academic pages: Publications, CV, Talks, Teaching, Blog (full academic site)
- B) Minimal: Publications, CV only (lean academic profile)
- C) Custom selection — please specify

**Why this matters**: Navigation determines visible site structure and which template demo pages need to be updated vs. deleted.

### Q2: How should we handle the CV page content?
**Options:**
- A) I provide all my real CV information (education, experience, skills) and you fill it in
- B) Remove the CV page entirely for now, re-add later when ready
- C) Create a CV page that links to a PDF download instead (provide PDF in `files/`)

**Why this matters**: The CV page is the most embarrassing issue — it shows fake template data. We need to know whether to populate or remove it.

### Q3: Should template demo content (talks, teaching, portfolio, blog posts) be deleted or kept as structure?
**Options:**
- A) Delete all demo content — I'll add real content later when I have it
- B) Keep the structure files but clear the content (empty collections)
- C) Only keep specific sections (specify which)

**Why this matters**: Demo content from 2012-2014 makes the site look unfinished and can confuse visitors.

## Identified Risks
- **Credibility risk**: Template placeholder content (especially CV) severely damages academic credibility if a reviewer/collaborator visits the site
- **SEO risk**: Key pages excluded from sitemap; no site verification configured
- **Performance risk**: 610KB profile image causes slow load on mobile
- **Consistency risk**: Publications exist in two places with different content and formatting

## AI-Slop Patterns Detected
- **Scope inflation risk**: Temptation to redesign the entire theme — user asked for review/optimization, not a redesign
- **Over-engineering risk**: Don't add complex features (blog, fancy animations) — keep it academic and clean

## Directives for Prometheus

### Core Directives
- MUST: Fix navigation (`_data/navigation.yml`) based on user's answer to Q1
- MUST: Fix timezone to `Asia/Shanghai`
- MUST: Fix typos and grammar in `about.md`
- MUST: Sync publications between `about.md` and `_pages/publications.md`
- MUST: Remove `sitemap: false` from about.md and publications.md
- MUST: Handle CV page based on user's answer to Q2
- MUST: Handle demo content based on user's answer to Q3
- MUST: Optimize profile image (compress to <100KB)
- MUST: Fix or remove analytics configuration
- MUST: Remove template demo pages (`markdown.md`, `archive-layout-with-content.md`, `terms.md`, `non-menu-page.md`)
- MUST NOT: Change the Jekyll theme or template structure
- MUST NOT: Add new features not requested
- MUST NOT: Modify `_sass/` or `_layouts/` or `_includes/` unless strictly necessary
- MUST NOT: Touch `.git/` or commit anything
- PATTERN: Follow existing academicpages conventions for any new content

### QA/Acceptance Criteria Directives (MANDATORY)
- MUST: Verify Jekyll builds without errors: `bundle exec jekyll build 2>&1 | tail -20`
- MUST: Verify navigation links render: grep for nav items in `_site/index.html`
- MUST: Verify sitemap includes key pages: `grep -c "about\|publications" _site/sitemap.xml`
- MUST: Verify profile image is <100KB: `ls -la images/profile.jpg | awk '{print $5}'`
- MUST: Verify no template placeholder text remains: `grep -r "GitHub University" _pages/`

## Recommended Approach
Break the optimization into prioritized waves: (1) Critical fixes — navigation, CV, timezone, typos; (2) Content sync — publications consistency; (3) Cleanup — remove demo content and template pages; (4) Performance & SEO — image optimization, sitemap, analytics. Execute wave-by-wave with verification after each.

<!-- AGENT_COMPLETE -->
