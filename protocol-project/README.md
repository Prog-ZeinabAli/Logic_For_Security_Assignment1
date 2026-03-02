# Protocol Project Solution — 02244 Logic for Security

## Contents

- **report.tex** — LaTeX report (compile with `pdflatex report.tex` to get PDF)
- **lab_logbook.md** — Lab logbook documenting protocol development
- **AnB files:**
  - `OpenAuth_Simple.AnB` — Week 2 simplified version (A has key)
  - `OpenAuth_Full.AnB` — Full protocol (A has no key, uses shared secret)
  - `OpenAuth_Formats.AnB` — Type-flaw resistant (Week 4)
  - `OpenAuth_TLS.AnB` — TLS channel variant (Week 5)
  - `GetPublicKey.AnB` — Key lookup protocol (Week 4)

## Compiling the Report to PDF

If you have LaTeX installed:
```bash
pdflatex report.tex
pdflatex report.tex   # run twice for references
```

Alternatively, use an online LaTeX editor (Overleaf, etc.) or convert the .tex to PDF with another tool.

## Verifying with OFMC

```bash
ofmc --numSess 1 OpenAuth_Full.AnB
ofmc --numSess 2 OpenAuth_Full.AnB
```

## Hand-in Checklist

- [ ] Report (15 pages max)
- [ ] Lab logbook
- [ ] AnB files
- [ ] Update author names in report
- [ ] Add resources used
