---
name: quiz
description: Scope-first active quiz for code and document understanding. Use when the user wants to internalize code or academic material by answering probing questions about abstractions, usage, mechanisms, assumptions, claims, or failure modes, rather than just receiving polished summaries. Good for session-, file-, and repo-level understanding. Supports code files, Markdown, LaTeX, PDF, and DOCX. Avoid generic software-process trivia unless it is central to understanding.
---

# Quiz

This package adds a `/quiz` command for active understanding of code and documents. It opens a native Glimpse quiz window.

## When to use

Use this when the user wants:
- active engagement rather than passive summary consumption
- to build a mental model of code or academic material through retrieval / prediction / explanation
- to understand a file, session, or codebase in a more tactile way
- to learn core abstractions, interfaces, mechanisms, assumptions, and change impact
- to critically read a paper or thesis by probing claims, methods, evidence, and assumptions
- to answer a question first, then discuss that specific question further in a focused follow-up thread

## Command surface

```text
/quiz
/quiz workset
/quiz session
/quiz repo
/quiz file <path>
/quiz --file <path>
/quiz --file paper.pdf --mode reviewer
/quiz --file thesis.tex --focus "the introduction and model formulation"
/quiz repo --audience scientist
/quiz repo --mode sci
/quiz-close
```

## Question style

The tutor should prefer questions that probe:
- what the abstraction or claim is for
- how to use it correctly or what evidence supports it
- how it works internally or what methodology was used
- what assumptions or invariants matter
- what would change if some parameter / branch / interface / assumption changed
- how one would detect likely failure modes or weaknesses in the argument
- in plain, direct language rather than formal or overly clever wording

Audience profiles:
- `general` / `gen` — balanced, accessible questions
- `scientist` / `sci` — representation, quantities, transformations, assumptions, perturbations
- `developer` / `dev` — interfaces, control flow, contracts, extension points, debugging/refactoring
- `reviewer` / `rev` — claims, methodology, evidence, assumptions, argument structure, implications

After feedback is shown, the quiz UI can also open a short **Discuss further** thread anchored to that card.

At quiz completion, the UI can optionally generate a short **Wrap-up report** based on the user's answers and the tutor feedback, and save it to disk.

## Document support

- `.md` and `.tex` — read directly as text
- `.pdf` — extracted via `pdftotext` (best-effort; suggest preprocessing to `.md` if garbled)
- `.docx` — extracted via `pandoc` (best-effort; suggest preprocessing to `.md` if garbled)

## Focus

Use `--focus "..."` to steer questions toward specific sections or topics. It affects both source selection and question generation, so repo-level prompts like `--focus "how the solver advances the flow front"` or `--focus "common themes in the abstracts"` can narrow the quiz meaningfully.

Avoid trivia like:
- tests
- CI
- file layout
- naming conventions
- tooling minutiae
- citation style or formatting

unless those are genuinely central to understanding the scoped material.
