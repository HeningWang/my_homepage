# CV, Homepage, and Publication Links Design

## Goal

Update Hening Wang's academic CV and website for August 2026, surface the newest accepted and submitted work, and provide durable public links to publication artifacts.

## Content policy

- List the two CogSci 2026 proceedings papers as accepted or forthcoming until a proceedings landing page is verified.
- List the RSAcm contribution as an accepted talk at Linguistic Evidence 2026.
- List the expanded argumentative-language manuscript as submitted to *Cognition*.
- Keep the submitted *Cognition* manuscript private during review.
- Give public entries one appropriate artifact link: paper, poster, abstract, or video.
- Preserve the user's existing edits in `source/about/index.md`.

## New 2026 entries

1. Hening Wang, Daniel Lassiter, and Michael Franke. "When Correlation Means Causation: Pragmatic Factors Modulate Causal Implicatures in Decision-Making Contexts." CogSci 2026, accepted poster paper.
2. Fausto Carcassi, Hening Wang, Chris Cummins, and Michael Franke. "What Guides Utterance Choice in Argumentative Language Use?" CogSci 2026, accepted oral paper.
3. Hening Wang, Yuhan Guo, and Michael Franke. "From Controversy to Consensus: Modelling Community-Sensitive Common Ground Management in German Discourse Markers." Linguistic Evidence 2026, accepted talk.
4. Fausto Carcassi, Hening Wang, Chris Cummins, and Michael Franke. "What Guides Utterance Production and Interpretation in Argumentative Language Use?" Submitted to *Cognition*.

## Site structure

### Homepage

Refresh `source/index.md` as a compact academic landing page with:

- current PhD and LMBayes affiliation;
- research focus;
- an August 2026 CV link;
- links to the Publications, About, and Now pages;
- a short "Latest" section featuring the three 2026 acceptances.

### Publications page

Create `source/publications/index.md` with grouped sections:

- manuscripts under review;
- conference proceedings;
- accepted talks and posters;
- earlier publications and presentations.

Each public artifact uses a small text link such as `paper`, `poster`, `abstract`, or `video`. Status wording stays explicit.

### About page

Retain the current educational background and expanded publication history. Add the 2026 entries and route readers to the dedicated Publications page.

### Navigation

Add Publications to `source/_data/keep.yml` so it is available from every page.

## CV structure

Use `CV/main.tex` as the maintained source and generate `CV/Hening_Wang_CV.pdf`.

- Add current PhD education.
- Update the CV date to August 2026.
- Add a "Manuscripts under review" section for the *Cognition* submission.
- Add the two CogSci 2026 papers under Publications with accepted/forthcoming wording.
- Add the Linguistic Evidence 2026 talk under peer-reviewed presentations.
- Retain earlier entries while correcting visible typographical and grammatical errors touched by this update.

## Artifact and link strategy

- Keep the existing CV Google Drive file ID and replace its PDF version in place, preserving the public URL.
- Upload shareable camera-ready papers and the Xeliherb poster with stable descriptive filenames.
- Configure Drive access as "Anyone with the link" and viewer-only.
- Record Drive URLs directly in the Publications page and reuse them from the Homepage or About page.
- Keep local copies of linked artifacts under `CV/` or a release staging folder for reproducibility.

## Validation

- Compile the CV with LaTeX and verify page count, fonts, hyperlinks, missing references, and overflow warnings.
- Run the Hexo production build.
- Check generated navigation and links.
- Serve the site locally and inspect the homepage, About page, and Publications page at desktop and narrow viewport widths.
- Verify every public URL returns the intended PDF or poster.
- Review `git diff` so the user's pre-existing About-page edits remain intact.

