---
name: papertopatent
description: >-
  Convert an English scientific paper or manuscript into Chinese national
  invention patent application files. Use when the user provides an English
  paper, manuscript DOCX/PDF, figures, supplementary information, or patent
  templates and asks to produce Chinese invention patent drafts, claims,
  specification, drawings, abstract, or the four CN filing documents:
  100001权利要求书.docx, 100002说明书.docx, 100003说明书附图.docx, and
  100004说明书摘要.docx.
---

# Papertopatent

## Purpose

Transform an English research paper into a Chinese national invention patent filing package. The deliverable is four Word files:

- `100001权利要求书.docx`
- `100002说明书.docx`
- `100003说明书附图.docx`
- `100004说明书摘要.docx`

Use the workflow in `references/workflow.md` for detailed drafting rules and QA gates. Use `scripts/build_patent_submission.py` when structured content and figure paths are ready.

## Core Workflow

1. Read all user-provided files: paper, figures, supplementary information, videos, cover letter, patent template files, and prior draft if present.
2. Extract the invention, not the paper story: technical field, prior-art defects, structural features, preparation steps, applications, experimental effects, figures, and comparative examples.
3. Search and read Chinese patent prior art when network is available, prioritizing CN invention patents in similar material, process, device, and application directions. Do not fabricate prior art. If official CNIPA or patent pages are inaccessible, state the access limit and use available verifiable sources.
4. Draft the patent around protectable technical features:
   - claims define structure/process/device/use boundaries;
   - specification supports every claim with embodiments, examples, and effects;
   - drawings are separated into the drawings file;
   - abstract is concise and under 300 Chinese characters unless the user asks otherwise.
5. Generate the four filing files in `.docx` format. Keep claim and specification text justified. Keep document headers, major headings, figure captions, and abstract-figure labels centered when appropriate.
6. Verify structure before delivery: all four files exist, claims have no figures, specification has no inserted figures, drawings file contains all drawing images, abstract file contains one abstract figure, old template residue is absent, and all `.docx` files open.

## Patent Drafting Rules

- Write as a Chinese invention patent, not as an academic paper.
- Do not keep template example content. Only keep the template format if templates are supplied.
- Avoid overbroad claims already covered by prior art. If a field is crowded, narrow the independent claim around the actual combination of structural features, preparation steps, and application scenario.
- Put exact performance values mainly in embodiments/results or dependent claims, not as the only basis for the independent claim.
- Use comparative examples to prove inventive contribution. At minimum, include controls that remove each key component or structural feature.
- Do not put figures in the claims. Do not put experimental raw figure panels in the specification body when a separate drawings file is required.
- Use consistent terminology across claims, specification, abstract, and drawing captions.

## Output Format Rules

If the user supplies official/template files, inspect and match:

- page size and margins;
- header text such as `权利要求书`, `说明书`, `说明书附图`, `说明书摘要`;
- footer code if present;
- font size and line spacing;
- paragraph alignment.

If no template is supplied, use this default CN filing-like layout:

- A4 portrait;
- margins: top 25 mm, left 25 mm, right 15 mm, bottom 15 mm;
- Songti/宋体 for Chinese, Times New Roman for Latin text;
- 10.5 pt body text;
- 1.5 line spacing;
- body and claims justified;
- major section titles centered.

## When Using the Builder Script

Create a JSON file matching the schema described in `references/workflow.md`, then run:

```bash
python scripts/build_patent_submission.py --content content.json --figures figures --out output_dir
```

The script creates the four `.docx` files and performs basic structural checks. The model is still responsible for drafting accurate legal/technical content before running the script.

## Quality Gate

Before final response:

- Check the four output paths.
- Count claims and drawings.
- Confirm all outputs are `.docx`.
- Confirm body/claim paragraphs are justified.
- Confirm abstract text is no more than 300 Chinese characters unless explicitly waived.
- Confirm old template terms and irrelevant example content are absent.
- Try Word/LibreOffice render or open validation when available; if render is unavailable, report structural QA only.
