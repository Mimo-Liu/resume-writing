---
name: resume-tailor
description: Tailor a resume to a specific job ad while maintaining 100% authenticity
argument-hint: [resume_path] [job_ad_path]
---

# Resume Tailor

Tailor a candidate's resume to a specific job ad. Every change must remain authentic to the candidate's actual experience — never fabricate or exaggerate.

## Source of Truth

The **master resume** is at `/Users/jirongliu/Max/Development/Resume Writing/Resume_Master.docx`. This is the comprehensive, untrimmed version containing ALL experience, skills, achievements, and capabilities. Always start from the master resume when tailoring — never tailor from a previously tailored version.

During tailoring, if new capabilities, achievements, or improved phrasings surface that are not yet in the master, flag them with the user. The master should be updated to capture these additions so it remains the complete source of truth for future applications.

## Inputs

1. **Master resume** (`Resume_Master.docx`) — always start here
2. **Job ad file** (`.docx`) — the target job posting

## Process

Work through these steps **sequentially**. Do not proceed to the next step until the user approves the current one. Present changes clearly and let the user drive decisions.

### Step 1: Job Ad Analysis & Gap Identification

Extract from the job ad:
- **Technical & Hard Skills** — specific tools, techniques, methodologies named
- **Soft Skills & Competencies** — leadership, communication, stakeholder management
- **Industry/Regulatory Context** — sector, frameworks, compliance requirements

Map against the resume and identify:
- What's already strong (direct matches)
- What's understated (present but not well-framed)
- What's missing (not in the candidate's experience — do NOT fabricate)
- What's overemphasized relative to the role (candidates to de-emphasize)

**After Step 1 is approved**, update the Skills Gap Analysis Excel file at `/Users/jirongliu/Max/Development/Resume Writing/Skills_Gap_Analysis.xlsx`:
- **Skills Matrix** sheet: Add a new column for this job. For each skill, mark: ✓ (strong), ○ (present), △ (understated), or ✗ (gap). Add any new skills from the job ad that aren't yet in the matrix.
- **Gap Summary** sheet: Add rows for each new gap identified, with severity, the job name, and an action for how to address it.
- Use `openpyxl` to read/write the Excel file. Preserve existing formatting and color coding.

### Step 2: Professional Summary Overhaul

Rewrite the title and summary. Techniques:
- Change the professional title to closely mirror the target job title
- Front-load the most relevant experience and technical keywords
- Provide 2-3 variations (e.g., Highly Tailored, Balanced, Punchy)
- Wait for the user to pick one before proceeding

### Step 3: Areas of Expertise / Skills Section

Restructure the skills section. Techniques:
- Drop skills irrelevant to the target role
- Add job ad keywords that map to actual experience
- Consolidate similar skills to keep the list tight
- Format as a flowing paragraph with Wingdings separators (matching resume convention)
- Keep the section scannable for ATS

### Step 4: Professional Experience Reframing

This is the core step. Go role by role, starting with the most recent/most relevant. For each role:

- **Role description**: Reframe to lead with team leadership, analytics, and commercial outcomes where relevant
- **Reorder bullets** by relevance to the target role
- **Rewrite bullets** using job ad verbs and framing while keeping factual claims intact
- **Drop bullets** that are irrelevant (e.g., FS-specific governance for a healthcare role)
- **Add bullets** only when genuinely supported by experience described in the resume
- **Use specific numbers** where possible (team size, FTE hours saved, revenue impact)
- **Explicitly name tools** used to achieve outcomes

### Step 5: Education & Technology Stack

- Reorder tech stack categories so most role-relevant items appear first
- Add emerging categories not in the original (e.g., AI & Emerging Tech) if supported by experience
- Reorder education and qualifications by relevance
- Separate formal degrees from professional certifications

### Step 6: Final Polish & Build

Do a final quality pass then build the `.docx` file. Create a folder named after the role and company, copy the job ad in with a `Job Ad_` prefix, and save the tailored resume.

Key formatting conventions for the output `.docx`:
- Page: A4 (7562850 x 10693400 EMU), 0.5-inch margins (457200 EMU)
- Name: 24pt bold centered
- Contact: 10.5pt centered
- Title: 13pt, #44526A color, centered
- Section headers: white text on #44526A background, 12pt bold centered (use paragraph shading)
- Company names: 12pt, #44526A, centered (Heading 1 style)
- Job titles: 10pt on #D4DCE3 background (paragraph shading)
- Bullets: List Paragraph style with Wingdings 'l' dot separators in #1D4575, hanging indent
- Education/Tech labels: bold first part, regular rest, 10pt
- Tech stack: 2-column table with bold labels in column 1 and values in column 2

## Working with .docx Files

Use `python-docx` for normal files. For files that fail to parse, fall back to `lxml` on the ZIP's internal `word/document.xml`.

Extract full paragraph text:
```python
import zipfile
from lxml import etree

with zipfile.ZipFile('file.docx') as zf:
    doc_xml = zf.read('word/document.xml')
root = etree.fromstring(doc_xml)
nsmap = {'w': 'http://schemas.openxmlformats.org/wordprocessingml/2006/main'}
for para in root.findall('.//w:p', nsmap):
    texts = [t.text or '' for t in para.findall('.//w:r/w:t', nsmap)]
    print(repr(''.join(texts)))
```

Paragraph shading for section headers:
```python
from docx.oxml.ns import nsdecls
from docx.oxml import parse_xml
pPr = para._p.get_or_add_pPr()
shd = parse_xml(f'<w:shd {nsdecls("w")} w:val="clear" w:fill="44526A"/>')
pPr.append(shd)
```

Wingdings bullet separator in flowing text:
```python
sep = para.add_run(' l ')
sep.font.name = 'Wingdings'
sep.font.size = Pt(10)
sep.font.color.rgb = RGBColor(0x1D, 0x45, 0x75)
```

## Rules

- Never fabricate experience, metrics, or skills the candidate doesn't have
- Never overwrite the source resume file — always create a new file
- Present changes for user approval at each step — do not skip ahead
- Keep the original resume's formatting conventions (fonts, margins, shading, bullet style)
- When dropping bullets or skills, explain why so the user can make an informed decision
