# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This is a resume writing and job application workspace. It contains resume `.docx` files, job advertisement captures, and tailored resume outputs.

## File Organization

- **`Resume_Master.docx`** (root level): The comprehensive master resume — source of truth containing all experience, skills, and achievements. Always start from this file when tailoring. Update it when new capabilities or improved phrasings surface during tailoring.
- **Role+Company folders** (e.g., `Head of Data and Analytics - Bupa Australia/`): Each application gets its own folder containing the job ad (prefixed `Job Ad_`), the tailored resume, and optional cover letter.
- **`Resume backup/`**: Historical versions of resumes.
- **`.claude/`**: Project-level settings and skills.

## Document Formatting Convention

Resumes use a consistent visual format:
- Page: A4, 0.5-inch margins
- Name: 24pt bold centered
- Section headers: White text on dark blue (#44526A) background
- Company names: 12pt, #44526A color, centered
- Job titles: 10pt on light grey (#D4DCE3) background
- Bullets: Wingdings dot separators with hanging indent
- Education/Tech Stack: Body Text style with bold labels

When creating or modifying `.docx` files, use `python-docx` with raw XML manipulation for paragraph shading and Wingdings font runs. The reference formatting template is at `Resume_reference for formatting.docx` (when present).

## Resume Tailoring Workflow

When tailoring a resume for a specific job, follow these steps sequentially. Do not proceed to the next step until the user approves the current one:

1. **Job Ad Analysis & Gap Identification** — Extract technical skills, soft skills, and industry context from the job ad; map against the resume to identify gaps.
2. **Professional Summary Overhaul** — Rewrite the title and summary to align with the target role. Provide 2-3 variations.
3. **Areas of Expertise Optimization** — Restructure skills into role-specific categories, drop generic skills, add job ad keywords present in actual experience.
4. **Professional Experience Reframing** — Rewrite bullets to use job ad verbs, inject technical tool names, and contextualize transferable skills. Keep all claims authentic.
5. **Education & Technology Stack Reordering** — Prioritize most relevant qualifications and categorize tools logically.
6. **Final Polish** — Grammar, spelling, consistent tense, ATS-friendly formatting.

Core rule: Never fabricate experience or exaggerate claims. All tailoring must remain 100% authentic to the candidate's actual experience.

## Working with .docx Files

- Use `python-docx` for reading/writing `.docx` files.
- For files that `python-docx` cannot parse (corrupted ZIP references), fall back to `lxml` directly on the internal `word/document.xml` inside the ZIP archive.
- Always extract full paragraph text before editing — never rely on truncated previews.
- When creating a new formatted resume, build from scratch programmatically rather than templating from an existing file.
