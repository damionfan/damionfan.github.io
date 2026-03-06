# Homepage Optimization Plan

## TL;DR
> Optimize Shengyu Fan's GitHub Pages academic homepage. Fix 15 issues across navigation, content, SEO, performance, and template cleanup. Estimated effort: ~30 minutes of execution. 4 waves of changes.

## Context
- **Original Request**: Review the GitHub Pages homepage project and provide optimization suggestions
- **Metis Findings**: 4 critical, 6 important, 5 nice-to-have issues identified
- **User Decisions**: Nav=Publications+CV only (Q1:B), Remove CV page (Q2:B), Delete all demo content (Q3:A)

## Work Objectives

### Core Objective
Clean up, fix, and optimize the academic homepage at `https://damionfan.github.io` to present a professional, accurate, and performant site.

### Deliverables
- Working navigation with Publications and CV links
- Accurate, typo-free homepage content
- Synchronized publications (about.md is source of truth)
- Optimized profile image (<100KB)
- Correct timezone and SEO settings
- All template demo content removed

### Must Have
- Navigation enabled for Publications (primary content page)
- All typos and grammar fixed
- Timezone corrected to Asia/Shanghai
- Homepage and publications in sitemap
- Profile image compressed
- All template demo files deleted

### Must NOT Have (Guardrails)
- NO theme/template structure changes (_sass/, _layouts/, _includes/)
- NO new features (blog, comments, etc.)
- NO changes to `.git/` or automatic commits
- NO over-engineering — simple fixes only
- NO changing publication content/ordering — only fix formatting consistency

## Verification Strategy
> ZERO HUMAN INTERVENTION — all verification is agent-executed.
- **Test Decision**: None (static Jekyll site)
- **QA Policy**: File content verification via grep + Jekyll build test
- **LSP Available**: NO

### Verification Tools:
- `bundle exec jekyll build 2>&1` → exit code 0, no errors
- `grep` → verify content changes, no leftover placeholder text
- `ls -la` → verify image size
- File existence checks → verify demo content deleted

## Execution Strategy
```
Wave 1 (Config & Navigation): Task 1, 2, 3 (parallel — independent config files)
Wave 2 (Content Fixes): Task 4, 5 (parallel — different pages)
Wave 3 (Cleanup): Task 6, 7, 8 (parallel — independent deletions)
Wave 4 (Performance & SEO): Task 9, 10 (parallel — independent concerns)
Final Verification Wave: Build test + comprehensive checks
```

---

## TODOs

- [ ] 1. Enable Navigation Links
  **What to do**: Edit `_data/navigation.yml` to enable Publications link ONLY (CV is removed per user decision Q2:B):
  ```yaml
  main:
    - title: "Publications"
      url: /publications/
  ```
  **Must NOT do**: Do not add CV, Talks, Teaching, Blog, or any other nav links
  **Parallelization**: Wave 1 | Blocks: none | Blocked by: none
  **Code References**: `_data/navigation.yml:1-26` — currently all commented out
  **QA Scenarios**:
    Scenario: Only Publications nav link present
      Tool: grep
      Steps: `grep -c "title:" _data/navigation.yml`
      Expected: Output is `1`
      Evidence: Command output

- [ ] 2. Fix Timezone and Analytics Config
  **What to do**: In `_config.yml`:
  - Change `timezone: America/Los_Angeles` → `timezone: Asia/Shanghai`
  - Change `analytics.provider` from `"google-universal"` → `false` (since tracking_id is empty)
  **Must NOT do**: Do not modify any other config settings
  **Parallelization**: Wave 1 | Blocks: none | Blocked by: none
  **Code References**: `_config.yml:283` (timezone), `_config.yml:139` (analytics)
  **QA Scenarios**:
    Scenario: Timezone is Asia/Shanghai
      Tool: grep
      Steps: `grep "timezone" _config.yml`
      Expected: `timezone: Asia/Shanghai`
    Scenario: Analytics disabled
      Tool: grep
      Steps: `grep "provider" _config.yml | head -1`
      Expected: `provider: false`

- [ ] 3. Fix Sitemap Exclusions
  **What to do**:
  - In `_pages/about.md`: Remove `sitemap: false` from frontmatter
  - In `_pages/publications.md`: Remove `sitemap: false` from frontmatter
  **Must NOT do**: Do not change any other frontmatter fields
  **Parallelization**: Wave 1 | Blocks: none | Blocked by: none
  **Code References**: `_pages/about.md:8`, `_pages/publications.md:7`
  **QA Scenarios**:
    Scenario: Sitemap flag removed
      Tool: grep
      Steps: `grep -c "sitemap: false" _pages/about.md _pages/publications.md`
      Expected: 0 matches (no output or empty)

- [ ] 4. Fix Homepage Typos and Grammar
  **What to do**: In `_pages/about.md`:
  - Line 22: "finial year" → "final year"
  - Line 41: "One paper are accepted" → "One paper is accepted"
  - Line 42: "Two paper are accepted" → "Two papers are accepted"
  - Line 47: "Two paper are accepted" → "Two papers are accepted"
  **Must NOT do**: Do not change any publication content, links, or the bio text
  **Parallelization**: Wave 2 | Blocks: none | Blocked by: none
  **Code References**: `_pages/about.md:22,41,42,47`
  **QA Scenarios**:
    Scenario: No typos remain
      Tool: grep
      Steps: `grep -c "finial\|paper are" _pages/about.md`
      Expected: 0 matches

- [ ] 5. Sync Publications Page with Homepage
  **What to do**: Update `_pages/publications.md` to match `_pages/about.md` publications:
  - Use the same shields.io badge format as about.md
  - Add all missing 2025 papers (MICRO'25 HAWK, ISCA'25 FAST, ISCA'25 Neo, HPCA'25 WarpDrive)
  - Add CCS'25 paper (mentioned in News but not listed yet — add placeholder entry)
  - Add ASPLOS'26, HPCA'26 entries (mentioned in News but not listed — add placeholder entries)
  - Fix typo: "MCIRO2024" → "MICRO2024"
  - Keep NN23 and Taiyi (Arxiv24) entries
  - Remove the commented-out INS22 paper
  - Remove duplicate entries
  **Must NOT do**: Do not change any author lists, paper titles, or links — copy exactly from about.md
  **Parallelization**: Wave 2 | Blocks: none | Blocked by: none
  **Code References**: `_pages/publications.md:1-46`, `_pages/about.md:50-101`
  **QA Scenarios**:
    Scenario: All 2025 papers present
      Tool: grep
      Steps: `grep -c "2025" _pages/publications.md`
      Expected: At least 5 lines matching
    Scenario: MICRO typo fixed
      Tool: grep
      Steps: `grep "MCIRO" _pages/publications.md`
      Expected: No output (0 matches)

- [ ] 6. Remove CV Page
  **What to do**: 
  - Delete `_pages/cv.md` (100% placeholder content, user chose to remove)
  - Remove CV from navigation (ensure nav only has Publications)
  **Must NOT do**: Do not delete any other pages
  **Parallelization**: Wave 3 | Blocks: none | Blocked by: Task 1 (nav must be set first)
  **Code References**: `_pages/cv.md:1-65`
  **QA Scenarios**:
    Scenario: CV page removed
      Tool: test
      Steps: `test ! -f _pages/cv.md && echo "DELETED"`
      Expected: "DELETED"

- [ ] 7. Delete Template Demo Content
  **What to do**: Delete these template demo files/directories:
  - `_talks/2012-03-01-talk-1.md` and all other files in `_talks/`
  - `_teaching/2014-spring-teaching-1.md` and all other files in `_teaching/`
  - `_portfolio/portfolio-1.md` and all other files in `_portfolio/`
  - `_posts/2012-08-14-blog-post-1.md`
  - `_drafts/post-draft.md`
  **Must NOT do**: Do not delete the directories themselves — only the contents
  **Parallelization**: Wave 3 | Blocks: none | Blocked by: none
  **Code References**: `_talks/` (4 files), `_teaching/` (2 files), `_portfolio/` (2 files), `_posts/` (1 file), `_drafts/` (1 file)
  **QA Scenarios**:
    Scenario: Demo content deleted
      Tool: find
      Steps: `find _talks _teaching _portfolio _posts _drafts -name "*.md" 2>/dev/null | wc -l`
      Expected: 0

- [ ] 8. Delete Template Demo Pages
  **What to do**: Delete these unnecessary template pages from `_pages/`:
  - `_pages/markdown.md` (markdown guide demo)
  - `_pages/archive-layout-with-content.md` (template demo)
  - `_pages/terms.md` (template terms page)
  - `_pages/non-menu-page.md` (template demo)
  **Must NOT do**: Do not delete about.md, publications.md, 404.md, sitemap.md, or any .html pages
  **Parallelization**: Wave 3 | Blocks: none | Blocked by: none
  **Code References**: `_pages/markdown.md`, `_pages/archive-layout-with-content.md`, `_pages/terms.md`, `_pages/non-menu-page.md`
  **QA Scenarios**:
    Scenario: Demo pages deleted
      Tool: test
      Steps: `test ! -f _pages/markdown.md && test ! -f _pages/terms.md && echo "CLEAN"`
      Expected: "CLEAN"

- [ ] 9. Optimize Profile Image
  **What to do**: Compress `images/profile.jpg` to under 100KB while maintaining acceptable quality.
  Use ImageMagick or similar:
  ```bash
  cp images/profile.jpg images/profile.jpg.bak
  convert images/profile.jpg -resize 400x400 -quality 85 images/profile.jpg
  ```
  Target: <100KB, 400x400px resolution (sufficient for sidebar avatar)
  **Must NOT do**: Do not change the filename or format — must remain `profile.jpg`
  **Parallelization**: Wave 4 | Blocks: none | Blocked by: none
  **Code References**: `images/profile.jpg` (currently 610KB)
  **QA Scenarios**:
    Scenario: Image under 100KB
      Tool: stat
      Steps: `stat --format="%s" images/profile.jpg`
      Expected: Value less than 102400

- [ ] 10. Clean Up Unused Template Images
  **What to do**: Delete template demo images that are not used by the actual site:
  - `images/3953273590_704e3899d5_m.jpg` (Flickr placeholder)
  - `images/bio-photo.jpg` (template default)
  - `images/bio-photo-2.jpg` (template default)
  - `images/foo-bar-identity.jpg` (template demo)
  - `images/foo-bar-identity-th.jpg` (template demo)
  - `images/image-alignment-*.jpg` (template demo, 4 files)
  - `images/editing-talk.png` (template demo)
  - `images/paragraph-indent.png` (template demo)
  - `images/paragraph-no-indent.png` (template demo)
  Keep: `profile.jpg`, `profile2.png`, `site-logo.png`, `favicon.ico`, `safari-pinned-tab.svg`, `browserconfig.xml`, `manifest.json`, `mstile-*.png`
  **Must NOT do**: Do not delete profile.jpg, site-logo.png, favicon.ico, or any mstile/manifest/browserconfig files
  **Parallelization**: Wave 4 | Blocks: none | Blocked by: none
  **QA Scenarios**:
    Scenario: Demo images removed
      Tool: test
      Steps: `test ! -f images/foo-bar-identity.jpg && echo "CLEAN"`
      Expected: "CLEAN"

---

## Final Verification Wave
- [ ] F1. Jekyll Build Test — `bundle exec jekyll build 2>&1 | tail -5` → exit code 0
- [ ] F2. No Placeholder Text — `grep -r "GitHub University\|Skill 1\|Professor Git" _pages/ _data/` → no output
- [ ] F3. Navigation Works — `grep "Publications" _data/navigation.yml` → match found
- [ ] F4. Profile Image Size — `stat --format="%s" images/profile.jpg` → <102400
- [ ] F5. Sitemap Inclusion — `grep -c "sitemap: false" _pages/about.md _pages/publications.md` → 0

## Success Criteria
```bash
# All these must pass:
bundle exec jekyll build 2>&1 | tail -1       # → "done in X seconds"
grep -c "title:" _data/navigation.yml         # → 1 (Publications only, CV removed per Q2)
grep "timezone" _config.yml                    # → "timezone: Asia/Shanghai"
grep -c "finial\|paper are" _pages/about.md   # → 0
stat --format="%s" images/profile.jpg          # → <102400
find _talks _teaching _portfolio _posts _drafts -name "*.md" 2>/dev/null | wc -l  # → 0
test ! -f _pages/cv.md && echo "OK"           # → "OK"
test ! -f _pages/markdown.md && echo "OK"     # → "OK"
```

<!-- AGENT_COMPLETE -->
