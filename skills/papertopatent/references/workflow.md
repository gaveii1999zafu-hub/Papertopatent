# Papertopatent Workflow

## 1. Input Intake

Collect and inspect:

- English manuscript or paper (`.docx`, `.pdf`, Markdown, or pasted text);
- all main figures and supplementary figures;
- supporting information and methods;
- videos or demos if they show application scenarios;
- existing Chinese patent draft, if any;
- official format templates, if supplied.

Prefer local files over web search. Use web search only for current/verifiable patent prior art or when the user explicitly asks for online patent reading.

## 2. Extract the Invention

Create an internal invention map:

- Chinese invention title;
- technical field;
- prior-art defects;
- actual technical problem;
- core technical solution;
- key components/materials;
- preparation route;
- device or system structure;
- application scenarios;
- experimental support;
- comparative examples;
- drawing list and abstract drawing candidate.

For a paper, do not preserve the paper narrative. Convert from “result story” to “structure-method-effect” patent logic.

## 3. Prior-Art Reading

When possible, read at least 20 relevant Chinese invention patents before final claim strategy. Cover:

- same material class;
- same preparation mechanism;
- same device/use scenario;
- same performance function;
- same self-powered/sensing architecture if relevant.

Record what is already crowded and what combination remains distinctive. Do not claim broad concepts already disclosed by many patents.

## 4. Claim Strategy

Build claims in layers:

1. independent material/composition claim;
2. dependent structural/component claims;
3. independent preparation method claim;
4. dependent parameter/process claims;
5. independent product/device claim if relevant;
6. independent use/application claim if it has a specific scenario.

Strong Chinese invention patent claims usually protect reproducible technical features, not adjectives such as “high-performance” or “excellent”.

Avoid claim language such as “as shown in Figure...” in claims.

## 5. Specification Structure

Generate `100002说明书.docx` with:

- title;
- 技术领域;
- 背景技术;
- 发明内容;
- 附图说明;
- 具体实施方式;
- examples;
- comparative examples;
- test methods;
- test results.

No inserted figures in the specification body when a separate `说明书附图` file is required.

## 6. Drawings File

Generate `100003说明书附图.docx` separately.

Use main figures that support claims. If the source paper contains complex multi-panel scientific figures, keep them for draft use but recommend later conversion to patent drawings with numeric reference signs.

Include captions:

- 图1 ...
- 图2 ...
- ...

Keep drawings large, clear, separated, and centered. Avoid crowded figure text where possible.

## 7. Abstract File

Generate `100004说明书摘要.docx` with:

- one Chinese abstract paragraph;
- no heading before the abstract text unless the template requires it;
- no more than 300 Chinese characters by default;
- one abstract figure, preferably the figure showing the overall structure or application mechanism.

The abstract must mention technical field, technical problem, core solution, and main use. Do not write a paper-style abstract.

## 8. Four-File Output

Always output:

- `100001权利要求书.docx`
- `100002说明书.docx`
- `100003说明书附图.docx`
- `100004说明书摘要.docx`

If a legacy `.doc` template is supplied, still honor the user's current instruction. If the user requires `.docx`, output `.docx`.

## 9. Structural QA

Check:

- all files exist and are `.docx`;
- claims file has claims only and no figures;
- specification has required sections and no inserted figures;
- drawings file has expected image count;
- abstract file has exactly one abstract figure unless user requests otherwise;
- text uses justified alignment for body and claims;
- abstract length is under 300 Chinese characters;
- old template residue is absent;
- output files open in Word or python-docx; render visually if a renderer is available.

## 10. Content QA

Verify:

- every independent claim is supported by the specification;
- every claimed component appears in embodiments;
- every key effect is supported by a test or comparative example;
- figure numbers match captions and figure descriptions;
- terminology is consistent;
- no unsupported numerical values are invented;
- limitations from prior art are reflected in claim narrowing.

## Suggested Content JSON Schema for the Builder

```json
{
  "title": "中文发明名称",
  "claims": ["1. ...", "2. ..."],
  "description": [
    {"type": "title", "text": "中文发明名称"},
    {"type": "heading", "text": "技术领域"},
    {"type": "paragraph", "text": "..."}
  ],
  "table": {
    "caption": "表1 ...",
    "rows": [["样品", "结构差异", "效果"], ["实施例1", "...", "..."]]
  },
  "drawings": [
    {"caption": "图1 ...", "file": "figure_1.png"},
    {"caption": "图2 ...", "file": "figure_2.png"}
  ],
  "abstract": {
    "text": "300字以内中文摘要",
    "figure": "abstract_figure.png"
  }
}
```
