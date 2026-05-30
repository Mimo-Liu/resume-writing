---
name: resume-tailor
description: Tailor a resume to a specific job ad while maintaining authenticity
argument-hint: [job_url_or_path]
---

# Resume Tailor

Tailor a candidate's resume to a specific job ad. Every change must remain authentic to the candidate's actual experience — never fabricate or exaggerate.

The candidate may grant a percentage flexibility (e.g., "20% flexibility") to align experience, skills, and capabilities to the target role. Flexibility means: framing analogous experience as transferable, softening gap severity, and using job-ad language more freely — but still never fabricating.

## Source of Truth

The **master resume** is at `/Users/jirongliu/Max/Development/Resume Writing/Resume_Master.docx`. This is the comprehensive, untrimmed version containing ALL experience, skills, achievements, and capabilities. Always start from the master resume when tailoring — never tailor from a previously tailored version.

During tailoring, if new capabilities, achievements, or improved phrasings surface that are not yet in the master, note them. After all tailoring steps are complete, update the master resume and Skills Gap Analysis to capture these improvements so they remain available for future applications.

## Formatting Reference

The canonical formatting reference is the USyd tailored resume at:

```
Head of Student Insights and Analytics - University of Sydney/Resume_Max Liu_Head of Student Insights and Analytics.docx
```

Always extract formatting from this file when building a new resume — it is the gold standard. Do not rely on hardcoded sizes in this skill file; they may drift. Verify against the reference.

## Inputs

1. **Master resume** (`Resume_Master.docx`) — always start here
2. **Job ad** — either a `.docx` file path or a LinkedIn job URL (fetch via WebFetch)

If the job ad is a LinkedIn URL, save the fetched content as a `.docx` in the application folder alongside the tailored resume.

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
- Change the professional title to closely mirror the target job title, but avoid copy-pasting it verbatim — adapt the language (e.g., "Head of" can become "Leader of")
- Front-load the most relevant experience and technical keywords from the job ad
- Surface any personal connections to the organization (e.g., alumni status)
- Provide 2-3 variations (e.g., Highly Tailored, Balanced, Punchy)
- Wait for the user to pick one before proceeding

### Step 3: Areas of Expertise / Skills Section

Restructure the skills section. Techniques:
- Drop skills irrelevant to the target role
- Add job ad keywords that map to actual experience
- Consolidate similar skills to keep the list tight
- Format as a flowing paragraph with Wingdings separators (matching resume convention)
- Keep the section scannable for ATS
- Drop skills that are already covered in the Tech Stack section (avoid duplication)

### Step 4: Professional Experience Reframing

This is the core step. Go role by role, starting with the most recent/most relevant. For each role:

**Before reordering bullets, rank the job requirements by importance.** This ranking drives the bullet order. Use three lenses:

1. **Frequency** — how many times each requirement is mentioned across both the responsibilities and requirements sections
2. **Position** — where it appears (earlier = more important; requirements section carries more weight than responsibilities)
3. **Language strength** — the phrasing used: "Must" > "Proven track record" > "Demonstrated ability" > "Strong" > "Experience" > "is advantageous"

Assign each requirement a theme (e.g., "Advisory & Influencing", "Innovation & Thought Leadership", "Team Leadership & Capability Uplift") and produce a ranked list. Present this to the user for approval before reordering bullets.

**Then reorder bullets for each role**, placing bullets that demonstrate higher-ranked themes first. A bullet that directly matches a specific job requirement but supports a lower-ranked theme (e.g., reporting uplift at #5) should appear AFTER bullets that demonstrate higher-ranked themes (e.g., senior leadership at #1, advisory at #2).

For each role:
- **Role description**: Reframe to lead with team leadership, analytics, and commercial outcomes where relevant
- **Reorder bullets** following the theme ranking — highest-priority themes first
- **Rewrite bullets** using job ad verbs and framing while keeping factual claims intact
- **Drop bullets** that are irrelevant (e.g., FS-specific governance for a healthcare role)
- **Add bullets** only when genuinely supported by experience described in the resume
- **Use specific numbers** where possible (team size, FTE hours saved, revenue impact)
- **Explicitly name tools** used to achieve outcomes
- **Bullet style**: The most recent/most relevant role (primary role) uses bold summary prefixes on each bullet (e.g., "Led Institution-Wide Uplift of Reporting and Visualisation Practices: ..."). All other roles use plain bullets without summary prefixes — the body text stands alone

### Step 5: Education & Technology Stack

- Reorder tech stack categories so most role-relevant items appear first
- Merge similar categories to reduce rows (e.g., "Data Viz & Reporting" + "Analytics, Data Science & Platforms" → "Analytics, Data Platforms & Visualisation")
- Generalize organization-specific platform names where appropriate (e.g., "Corporate Data Hub" → "Data Warehouse")
- Add emerging categories not in the original (e.g., AI & Emerging Tech) if supported by experience
- Reorder education and qualifications by relevance; front-load any connection to the hiring institution
- Separate formal degrees from professional certifications

### Step 6: Final Polish & Build

Do a final quality pass then build the `.docx` file. Create a folder named after the role and company, copy the job ad in with a `Job Ad_` prefix, and save the tailored resume.

**Quality checks before finalizing:**
- Run a formatting review on the `.docx` — verify section header shading, Wingdings bullets, company name colors, job title backgrounds, and role description italics are all present
- Check for formatting leaks: contact line should NOT be bold or italic; name should be bold only (not italic); title and company names should be bold only (not italic)
- Check for double spaces (common in tech stack label runs)
- Verify consistent spelling (Australian English: "organisation" not "organization", "visualisation" not "visualization")
- Scan for residual industry jargon from the candidate's current sector that doesn't apply to the target role
- Run a character count to estimate page length (target: 2-3 pages)

**If small edits are needed after the initial build**, patch the raw XML directly via `lxml` rather than rebuilding from scratch. For systemic formatting issues (wrong font sizes across the entire document), rebuild — don't patch.

## Formatting Conventions

Extract exact font sizes, spacing, and colors from the USyd reference resume before building. Key conventions verified against the reference:

**Page Setup:**
- A4 (11907000 x 16840000 EMU), 0.5-inch margins (Inches)

**Elements (verified against USyd reference):**
- Name: 36pt bold centered — bold only, never italic
- Contact: 16pt regular centered — no bold, no italic
- Title: 20pt bold, #44526A, centered — bold only, never italic
- Summary: 14pt regular, before=80 after=40
- Section headers: 20pt bold, white text on #44526A background, centered, before=240 after=60
- Areas of Expertise: 14pt flowing paragraph, Wingdings 'l' separators in #1D4575, before=80 after=40
- Company names: 20pt bold, #44526A, centered, before=200 after=0 — bold only, never italic
- Job titles: 16pt bold on #D4DCE3 background (paragraph shading), centered, before=0 after=40
- Role descriptions: 14pt italic, left indent (360 twips), before=40 after=120
- Primary bullets (most recent role): 14pt, Wingdings 'l' dot in #1D4575, left=360 hanging=180, before=120 after=120. Bold summary prefix ending with `: ` then regular body text
- Secondary bullets (other roles): 14pt, Wingdings 'l' dot in #1D4575, left=374 hanging=187, before=120 after=120. All regular text — no bold prefix
- ADDITIONAL EXPERIENCE header: 14pt bold, left-aligned, NO blue shading (not a section header)
- Additional role job title: 14pt regular, left indent, NO #D4DCE3 shading (not a main job title)
- Education sub-headers ("EDUCATION", "PROFESSIONAL QUALIFICATIONS"): 14pt bold, before=0 after=0
- Education items: 14pt regular, left indent — NOT italic
- Professional Qualifications items: 14pt italic, left indent, before=40 after=120
- Tech stack: 14pt, bold label run + regular value run, before=0 after=0
- References: 14pt italic, centered

**Colors:**
- Dark blue: #44526A (section headers, company names, title)
- Dot blue: #1D4575 (Wingdings bullets and AoE separators)
- White: #FFFFFF (section header text)
- Light grey background: #D4DCE3 (job title paragraph shading)
- Dark blue background: #44526A (section header paragraph shading)

## python-docx Boolean Trap

**Never set `run.bold = False` or `run.italic = False`.** python-docx creates `<w:b w:val="false"/>` or `<w:i w:val="false"/>` elements which still register as bold/italic formatting. This causes invisible style leaks that are hard to diagnose.

```python
# WRONG — creates unwanted w:i element
run.italic = False

# RIGHT — only set when True, omit otherwise
if italic:
    run.italic = True
```

Same rule applies to `run.bold`. Always wrap in `if bold:` / `if italic:` conditions.

## Post-Tailoring: Update Master Resume & Skills Gap Analysis

After all tailoring steps are complete and the output is approved, update these files so improvements feed back into the source of truth:

**Resume_Master.docx:**
- Add any new Areas of Expertise phrasings that surfaced during tailoring (but keep ALL existing skills — the master is the comprehensive superset). Insert new items alongside related existing items for logical grouping
- Reorganize Tech Stack to match improved category structure from the tailoring. Merge similar rows to reduce category count
- Do NOT add role-specific summary or bullet changes — the master retains its original comprehensive bullets

**Skills_Gap_Analysis.xlsx:**
- Skills Matrix: Add a new column for this job with ratings for all existing and new skills. Add rows for any new skills surfaced by the job ad
- Gap Summary: Add rows for each identified gap with severity, the job name, and a detailed action plan for how to address it
- Use `openpyxl` and preserve existing formatting
- Use `insert_rows()` rather than shifting cells manually to avoid StyleProxy errors

## Working with .docx Files

Build new files with `python-docx`. For files that fail to parse or need surgical fixes, fall back to `lxml` on the ZIP's internal `word/document.xml`.

**Always use the correct XML namespace for xml:space:**
```python
t.set('{http://www.w3.org/XML/1998/namespace}space', 'preserve')
```
Never use `{http://schemas.xml:lang}space` — it is not a valid URI and will corrupt the document.

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

Bullet indent (hanging indent via raw XML):
```python
ind = parse_xml(f'<w:ind {nsdecls("w")} w:left="360" w:hanging="180"/>')
pPr.append(ind)
```

Patching raw XML after build (for surgical fixes):
```python
import zipfile, io
from lxml import etree

with zipfile.ZipFile(path, 'r') as zf:
    doc_xml_str = zf.read('word/document.xml').decode('utf-8')
    files = {name: zf.read(name) for name in zf.namelist()}

root = etree.fromstring(doc_xml_str.encode('utf-8'))
nsmap = {'w': 'http://schemas.openxmlformats.org/wordprocessingml/2006/main'}

# Find and fix specific elements...
# For removing bold from a run:
#   rPr = run.find('.//w:rPr', nsmap)
#   b = rPr.find('.//w:b', nsmap)
#   if b is not None: rPr.remove(b)

new_xml = etree.tostring(root, xml_declaration=True, encoding='UTF-8', standalone=True)
files['word/document.xml'] = new_xml
buf = io.BytesIO()
with zipfile.ZipFile(buf, 'w', zipfile.ZIP_DEFLATED) as out:
    for name, data in files.items():
        out.writestr(name, data)
with open(path, 'wb') as f:
    f.write(buf.getvalue())
```

## Rules

- Never fabricate experience, metrics, or skills the candidate doesn't have
- Never overwrite the source resume file — always create a new file
- Present changes for user approval at each step — do not skip ahead
- Keep the original resume's formatting conventions (fonts, margins, shading, bullet style)
- When dropping bullets or skills, explain why so the user can make an informed decision
- Use Australian English spelling ("organisation", "visualisation", "utilisation") — consistent across all output
- After tailoring is complete, feed back improvements to Resume_Master.docx and Skills_Gap_Analysis.xlsx
- Match the USyd reference resume formatting exactly — extract and verify, don't assume
- Rebuild from scratch for systemic formatting fixes; patch raw XML only for small surgical changes
- Never set `run.bold = False` or `run.italic = False` in python-docx — conditionally set True only
