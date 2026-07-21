# CEMA — Introduction to Probability (WebR / quarto-live)

Interactive lecture notes for **Foundations for Public Health & Epidemiological
Data Analysis**, styled to match the CEMA 2024 template. Every R block runs in
the browser via WebR — no local R needed by students.

Structure follows the course PowerPoint (slides 15–19): probability terminology,
set operations, definition of probability, mutually exclusive events, and
conditional probability — then extends into **Bayes' theorem / diagnostic
testing** and **random variables (expectation & variance)**. Enriched with
material from OpenIntro Statistics, Ch. 3 (smallpox 1721, diagnostic testing).
`iris` is used as a neutral warm-up; the substantive examples use a simulated
epidemiological `cohort` (smoking exposure → disease outcome).

## Files

| File | Purpose |
|---|---|
| `Probability.qmd` | The slides (content + live WebR cells) |
| `cema.scss` | CEMA 2024 theme (Africa hero left, grey title rule, logo lockup) |
| `header.html` | Small font-rendering tweaks |
| `assets/africa_orange.png` | Orange Africa graphic (from the .potx) |
| `assets/cema_logo.png` | CEMA + University of Nairobi logo lockup |

## One-time setup (on your Mac)

Install Quarto, then add the **quarto-live** extension inside this folder:

```bash
cd cema-probability
quarto add r-wasm/quarto-live
```

## Render / preview

```bash
quarto preview Probability.qmd      # live reload while editing
# or
quarto render  Probability.qmd      # produces Probability.html
```

### Important: the include line that makes code cells interactive

Right after the YAML, the document contains:

```
{{< include ./_extensions/r-wasm/live/_knitr.qmd >}}
```

This line **registers the `{webr}` engine** so the code cells render as runnable
editors. It requires:

- `engine: knitr` in the YAML (present), and R installed locally (for rendering only).
- The extension installed, i.e. the file `_extensions/r-wasm/live/_knitr.qmd`
  must exist. Confirm with `ls _extensions/r-wasm/live/`. If it's missing, run
  `quarto add r-wasm/quarto-live` again inside this folder.

Without this include, `{webr}` blocks appear as plain, non-runnable code.

## Notes for teaching

- The **"Our working example"** slide has a cell marked `#| autorun: true`; it
  builds the `cohort` data frame when the page loads, so later cells can use it.
  All examples use **base R only**, so WebR starts quickly (no package download).
- Other cells use `#| autorun: false` — students press **Run** (edit first if
  they like). Set a cell to `autorun: true` to have it execute on load.
- All numeric outputs in the notes were verified against R 4.3.3
  (e.g. prevalence 0.172, risk ratio 3.54, PPV 4.3%, smallpox 1-in-40 vs 1-in-7).
- Add `#| exercise: some-id` to turn a cell into a graded exercise (see the
  quarto-live docs for hints/solutions).
- Section dividers use `# Title {.section-slide background-image="assets/africa_orange.png" ...}`.
- Theme knobs live near the top of `cema.scss`: `$logo-height` (logo size) and
  `$hero-text-shift` (how far title/section text clears the Africa map).
