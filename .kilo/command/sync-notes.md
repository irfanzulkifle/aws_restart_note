Process newly added daily notes in `daily_notes/`. Find any files that exist in the main repo at `D:\git\aws_restart_note\daily_notes` but not yet in the worktree at `D:\git\aws_restart_note\.kilo\worktrees\six-booklet\daily_notes`. For each new file (and any existing files in the same week that need standardizing):

1. **Copy to worktree** and **standardize format**:
   - Header: `# Lecture Notes — Month DD, YYYY`
   - Cohort: `**Cohort 3 | Project CloudIgnite**`
   - Topics: `**Topics:** [comma-separated, no emoji, no · ]`
   - Duration: `**Duration:** ~3 hours`
   - Remove any blockquote CLF-C02 notices at the top
   - Remove any emoji from headers (📚, 🎯, ✅, ⚠️, etc.)
   - Remove any `## Topics Covered` sections (duplicates `## Table of Contents`)
   - Add `## Key Takeaways` section (6–8 bullet points) between header metadata and `---` separator before ToC
   - Ensure Table of Contents links match actual section headings

2. **Create or update `week_X/weekly_summary.md`**:
   - If new week: create from scratch using template from existing weeks (same structure: H1 with date range, "What We Learned" with subsections per day, "Key CLF-C02 Connections", "Daily Notes" list)
   - If existing week: add section for new day(s), update H1 date range, add entry to Daily Notes list
   - Include tables, bold key terms, and bullet points — no paragraphs, no conversational filler

3. **Update `daily_notes/weekly_summary_index.md`**:
   - Add/modify week row in the table (Week | Dates | Key Topics | Summary)
   - Update Learning Journey Overview to include new week
   - Ensure all weeks from 3 to current are present and in order

4. **Update `README.md`**:
   - `**Current Week:**` to latest week number
   - `**Total Daily Notes:**` recount all `.md` files across all `week_*` folders (exclude weekly_summary files from the count)
   - Repository Structure: add new daily notes under their week, add new week folders if needed

5. **Update `exam_prep/clf_c02_cheatsheet.md`**:
   - Add new CLF-C02 relevant concepts as numbered entries at the end of "Common Exam Gotchas" (continue from #41+)
   - Update footer: `*Last updated: Month DD, YYYY*`
   - Update scope header if needed: `(Weeks 3–XX)`

6. **Git operations**: stage all changes, commit with message `Add Week X: [topics]`, switch to main (clean untracked conflicts first), merge six-booklet, push to origin/main
