# CV, Homepage, and Publication Links Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use $superpower-subagents (recommended) or $superpower-executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking via update_plan.

**Goal:** Publish an August 2026 academic CV and an updated Hexo homepage with durable Google Drive links for the newest public papers and poster.

**Architecture:** Maintain the CV in LaTeX, keep publication prose in one dedicated Markdown page, and use the homepage as a concise entry point. Public PDFs live in the existing Google Drive `My Drive/Homepage` folder; Drive item IDs become stable website links. Hexo continues to publish the website from the `gh-pages` branch.

**Tech Stack:** LaTeX, Hexo 7, Markdown, YAML, Google Drive for desktop, GitHub Pages

---

## File map

- Modify `CV/main.tex`: maintained CV source.
- Create `CV/Hening_Wang_CV.pdf`: compiled August 2026 CV.
- Create `release/google-drive/README.md`: artifact names, source paths, Drive targets, and public URLs.
- Modify `source/index.md`: concise academic homepage and latest work.
- Create `source/publications/index.md`: complete publication and presentation list.
- Modify `source/about/index.md`: preserve the user's edited biography and add 2026 links.
- Modify `source/_data/keep.yml`: add Publications to global navigation.
- Modify `.github/workflows/deploy.yml`: publish this repository to its own `gh-pages` branch.

### Task 1: Establish the release manifest

**Files:**
- Create: `release/google-drive/README.md`

- [ ] **Step 1: Record the exact public artifacts**

Create the manifest with these source-to-target mappings:

```text
CV/Hening_Wang_CV.pdf
  -> My Drive/Homepage/CV_Wang_2026_02_06.pdf

/Users/heningwang/Documents/GitHub/Xeliherb/writing/Xeliherb_CogSci_camera_ready/main.pdf
  -> My Drive/Homepage/Wang_Lassiter_Franke_2026_CogSci_Paper.pdf

/Users/heningwang/Documents/GitHub/Xeliherb/writing/poster_cogsci/Xeliherb_CogSci_2026/main.pdf
  -> My Drive/Homepage/Wang_Lassiter_Franke_2026_CogSci_Poster.pdf

/Users/heningwang/Documents/GitHub/argumentative_language/paper_CogSci-2026/RSArg-CogSci-2026.pdf
  -> My Drive/Homepage/Carcassi_Wang_Cummins_Franke_2026_CogSci_Paper.pdf
```

The manifest must state that the submitted *Cognition* manuscript remains private and that the Linguistic Evidence abstract will receive a public link after its final conference version is prepared.

- [ ] **Step 2: Verify every source artifact**

Run:

```bash
pdfinfo /Users/heningwang/Documents/GitHub/Xeliherb/writing/Xeliherb_CogSci_camera_ready/main.pdf
pdfinfo /Users/heningwang/Documents/GitHub/Xeliherb/writing/poster_cogsci/Xeliherb_CogSci_2026/main.pdf
pdfinfo /Users/heningwang/Documents/GitHub/argumentative_language/paper_CogSci-2026/RSArg-CogSci-2026.pdf
```

Expected: each existing publication artifact reports a positive page count and no syntax error. The new CV is verified immediately after compilation in Task 2.

### Task 2: Update and compile the CV

**Files:**
- Modify: `CV/main.tex`
- Create: `CV/Hening_Wang_CV.pdf`

- [ ] **Step 1: Add current status and PhD education**

Add `Last updated: August 2026` to the heading and insert this education entry above the MA:

```latex
\resumeSubheading
  {University of T\"ubingen}{T\"ubingen, Germany}
  {Ph.D. candidate in General Linguistics}{Apr. 2024 -- Present}
```

- [ ] **Step 2: Add the submitted manuscript**

Insert a `Manuscript Under Review` section before Publications:

```latex
\section{Manuscript Under Review}
\begin{description}
\item {Fausto Carcassi$^*$, \textbf{Hening Wang}$^*$, Chris Cummins, \& Michael Franke (2026). What guides utterance production and interpretation in argumentative language use? Submitted to \textit{Cognition}. $^*$Equal contribution.}
\end{description}
```

- [ ] **Step 3: Add the accepted CogSci papers**

Place both entries at the beginning of Publications:

```latex
\item {\textbf{Hening Wang}, Daniel Lassiter, \& Michael Franke (2026). When correlation means causation: Pragmatic factors modulate causal implicatures in decision-making contexts. Accepted for publication in the \textit{Proceedings of the Annual Meeting of the Cognitive Science Society}.}

\item {Fausto Carcassi, \textbf{Hening Wang}, Chris Cummins, \& Michael Franke (2026). What guides utterance choice in argumentative language use? Accepted for publication in the \textit{Proceedings of the Annual Meeting of the Cognitive Science Society}.}
```

- [ ] **Step 4: Add the 2026 presentations**

Place these entries at the beginning of Peer-Reviewed Posters and Presentations:

```latex
\item {\textbf{Hening Wang}, Yuhan Guo, \& Michael Franke (2026). From controversy to consensus: Modelling community-sensitive common ground management in German discourse markers. Talk accepted at Linguistic Evidence 2026, Mannheim.}

\item {Fausto Carcassi, \textbf{Hening Wang}, Chris Cummins, \& Michael Franke (2026). What guides utterance choice in argumentative language use? Oral presentation at CogSci 2026, Rio de Janeiro.}

\item {\textbf{Hening Wang}, Daniel Lassiter, \& Michael Franke (2026). When correlation means causation: Pragmatic factors modulate causal implicatures in decision-making contexts. Poster presented at CogSci 2026, Rio de Janeiro.}
```

- [ ] **Step 5: Correct touched CV copy**

Use `Research Assistant`, `Bayesian modeling`, `PyTorch`, `Git`, `Tübingen`, `Utrecht University`, `contrastive study`, `an experimental study`, and `precedence precedes dominance`. Convert date ranges in touched entries to en-dash style.

- [ ] **Step 6: Compile the CV**

Run:

```bash
cd CV
latexmk -pdf -interaction=nonstopmode -halt-on-error -jobname=Hening_Wang_CV main.tex
```

Expected: exit 0 and `CV/Hening_Wang_CV.pdf` exists.

- [ ] **Step 7: Inspect the CV build log**

Run:

```bash
rg -n 'LaTeX Warning|Overfull|Underfull|undefined|Error' CV/Hening_Wang_CV.log
pdfinfo CV/Hening_Wang_CV.pdf | rg 'Pages|Page size|File size'
pdftotext CV/Hening_Wang_CV.pdf - | sed -n '1,220p'
```

Expected: no undefined references or LaTeX errors; each new title appears in extracted text.

### Task 3: Upload artifacts through Google Drive for desktop

**Files:**
- Modify: `release/google-drive/README.md`
- External targets: `/Users/heningwang/Library/CloudStorage/GoogleDrive-hening.wang0615@gmail.com/My Drive/Homepage/*.pdf`

- [ ] **Step 1: Replace the existing CV in place**

Copy `CV/Hening_Wang_CV.pdf` over `CV_Wang_2026_02_06.pdf`. Verify that the target retains Drive item ID `1VdAp3BVTvZCSXBJUOxJucXfEOKgTeMN5` using:

```bash
xattr -p 'com.google.drivefs.item-id#S' '/Users/heningwang/Library/CloudStorage/GoogleDrive-hening.wang0615@gmail.com/My Drive/Homepage/CV_Wang_2026_02_06.pdf'
```

- [ ] **Step 2: Copy the three new public artifacts**

Copy each source from Task 1 to its descriptive target name in the Drive Homepage folder.

- [ ] **Step 3: Capture stable public URLs**

Wait for each new target to receive a `com.google.drivefs.item-id#S` extended attribute. Record links in this form:

```bash
for target in \
  '/Users/heningwang/Library/CloudStorage/GoogleDrive-hening.wang0615@gmail.com/My Drive/Homepage/Wang_Lassiter_Franke_2026_CogSci_Paper.pdf' \
  '/Users/heningwang/Library/CloudStorage/GoogleDrive-hening.wang0615@gmail.com/My Drive/Homepage/Wang_Lassiter_Franke_2026_CogSci_Poster.pdf' \
  '/Users/heningwang/Library/CloudStorage/GoogleDrive-hening.wang0615@gmail.com/My Drive/Homepage/Carcassi_Wang_Cummins_Franke_2026_CogSci_Paper.pdf'
do
  drive_id=$(xattr -p 'com.google.drivefs.item-id#S' "$target")
  printf '%s\thttps://drive.google.com/file/d/%s/view?usp=sharing\n' "$target" "$drive_id"
done
```

- [ ] **Step 4: Verify anonymous access**

Use an unauthenticated HTTP request for each URL and confirm that Google returns a file-view page. If the Drive Homepage folder does not propagate public viewer access, open the folder's sharing controls and set `Anyone with the link` to `Viewer`, then repeat the checks.

### Task 4: Build the Publications page

**Files:**
- Create: `source/publications/index.md`

- [ ] **Step 1: Add page metadata and status sections**

Use this structure:

```markdown
---
title: publications
date: 2026-08-02 00:00:00
---

## Manuscript under review

## Conference proceedings

## Accepted talks and posters

## Earlier publications

## Earlier presentations
```

- [ ] **Step 2: Add the four 2026 research entries**

Add the *Cognition* manuscript with status text only. Add `paper` links to both CogSci entries, a `poster` link to the Xeliherb entry, and `abstract forthcoming` text to the Linguistic Evidence entry.

- [ ] **Step 3: Migrate the existing earlier entries**

Copy the 2022--2025 publication and presentation entries from `source/about/index.md`. Preserve the existing Drive links for the 2024 CORE poster and 2022 AMLaP video/poster/abstract where they remain available.

### Task 5: Refresh the homepage, About page, and navigation

**Files:**
- Modify: `source/index.md`
- Modify: `source/about/index.md`
- Modify: `source/_data/keep.yml`

- [ ] **Step 1: Replace the homepage body**

Keep the existing front matter and avatar. Use a first-person introduction with current PhD/LMBayes affiliation, a one-sentence research focus, direct links to CV and Publications, and a `Latest` section containing the three accepted 2026 contributions.

- [ ] **Step 2: Update About while preserving user edits**

Keep the February 2026 edits as the baseline, update the CV label to August 2026, add a link to `/my_homepage/publications/`, and add the four 2026 status entries. Keep the submitted manuscript unlinked.

- [ ] **Step 3: Add Publications navigation**

Insert this menu item between Posts and About:

```yaml
publications: /publications       || fa-solid fa-book-open
```

- [ ] **Step 4: Check internal and external URLs**

Run:

```bash
rg -n 'drive.google.com|/my_homepage/(publications|about|now)' source/index.md source/about/index.md source/publications/index.md
```

Expected: the CV URL retains its existing item ID and each public 2026 artifact has the Drive ID captured in Task 3.

### Task 6: Repair deployment and run production QA

**Files:**
- Modify: `.github/workflows/deploy.yml`

- [ ] **Step 1: Point deployment at this repository**

Change:

```yaml
PUBLISH_REPOSITORY: theme-keep/hexo-theme-keep-starter
```

to:

```yaml
PUBLISH_REPOSITORY: HeningWang/my_homepage
```

Remove the starter theme's `CNAME` line. Keep deployment to `gh-pages`.

- [ ] **Step 2: Build the site**

Run:

```bash
npm run build
```

Expected: exit 0 and generated files exist at `public/index.html`, `public/about/index.html`, and `public/publications/index.html`.

- [ ] **Step 3: Validate generated content**

Run:

```bash
rg -n 'CogSci 2026|Linguistic Evidence 2026|Cognition|PUBLICATIONS' public/index.html public/about/index.html public/publications/index.html
```

Expected: all four 2026 statuses appear and the Publications menu is rendered.

- [ ] **Step 4: Inspect desktop and narrow layouts**

Serve the generated site and capture the homepage, About page, and Publications page at approximately 1440 px and 390 px viewport widths. Check navigation wrapping, text overflow, link visibility, and headings.

- [ ] **Step 5: Commit the implementation**

```bash
git add CV/main.tex CV/Hening_Wang_CV.pdf release/google-drive/README.md source/index.md source/about/index.md source/publications/index.md source/_data/keep.yml .github/workflows/deploy.yml
git commit -m "feat: publish 2026 CV and research updates"
```

- [ ] **Step 6: Publish and verify**

Push `main`, let the deployment update `gh-pages`, and verify:

```text
https://heningwang.github.io/my_homepage/
https://heningwang.github.io/my_homepage/about/
https://heningwang.github.io/my_homepage/publications/
```

Expected: all three URLs return the new content and every Drive link opens the intended artifact.

## Verification summary

- CV compiles and contains all four 2026 status updates.
- Submitted manuscript has status text and no public manuscript URL.
- Existing CV Drive item ID is preserved.
- New CogSci paper/poster assets have stable Drive item IDs.
- Hexo build succeeds and generated pages contain the current entries.
- Deployment targets `HeningWang/my_homepage` and the live site reflects the build.

**Next skill:** `$superpower-executing-plans`
