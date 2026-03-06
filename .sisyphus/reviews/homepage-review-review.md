# Momus Review: homepage-review

## Verdict: [OKAY] ✅

Plan is executable. A competent developer can proceed without getting stuck.

### Verification Summary
- Verified 12/12 file references — all valid
- 10 tasks have clear acceptance criteria with specific grep/test commands
- Wave dependencies are logically consistent (Wave 3 Task 6 depends on Task 1 for nav — correct)
- QA scenarios are specific enough to execute (all use concrete tools + expected output)
- Collection demo content confirmed: 10 files across _talks/, _teaching/, _portfolio/, _posts/, _drafts/

### Minor Notes (Non-Blocking)
- Task 6 removes CV page but Task 1 enables CV nav link — slight contradiction. Since user chose Q2:B (remove CV), the nav in Task 1 should only include Publications, not CV. The Hephaestus executor should enable ONLY the Publications link in navigation, not CV.
- Task 5 mentions CCS'25 and ASPLOS'26/HPCA'26 as placeholders since the papers are in the News section but have no publication entries yet — this is fine, executor can add stub entries or skip if insufficient info.
- Task 9 uses ImageMagick `convert` — ensure it's installed, or use alternative compression tool.
- `_data/authors.yml` contains template placeholders but is not addressed in the plan — non-blocking since it's not user-facing when author_profile uses _config.yml settings.
- `_portfolio/` directory has a file `portfolio-2.md` not mentioned — should be caught by the `find` + delete pattern.

<!-- AGENT_COMPLETE -->
