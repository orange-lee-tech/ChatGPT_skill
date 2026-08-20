# Pixel Chronicle — PRODUCTION COMPACT
**Audience:** AI executor  
**Output:** square pixel images, default 1:1  
**Modes:** `narrative` | `factual`  
**Status:** frozen production baseline

## 1. CORE
- `narrative`: narrative owns meaning; facts are embedded into one coherent world.
- `factual`: facts own explanation; illustration serves fast understanding.
- **Text verifies. Visuals embody. Style serves content, never replaces it.**
- Never send this full Skill, QA notes, failure history, or reasoning context to the image model.

## 2. PIPELINE
`Lock scope → Lock facts → Lock golden reference → Choose one mode → Build short brief → Generate one image → Audit`

## 3. FACT LOCK
Internally resolve:
```yaml
subject:
scope:
time_range:
allowed_facts:
context_only:
excluded:
exact_strings:
```
Every important visible fact must pass: `TRUTH` supported; `SCOPE` belongs here; `BINDING` correct entity; `STATUS` correct state.
A true fact from another project/person/time is invalid here.
Do not invent names, domains, companies, dates, numbers, technologies, awards, locations, or status.
Do not print Skill/mode/QA/prompt/workflow terminology unless the user explicitly asks to visualize the method.

## 4. GOLDEN REFERENCE LOCK
If the user marks an image preferred, best, near-perfect, target, or “use this style”, treat it as `approved_golden_reference`.
If the tool supports references, pass the ACTUAL approved image into generation.
It strongly controls pixel scale, outline weight, shading depth, object volume, material richness, texture density, typography, composition maturity, decorative detail, and production quality.
It contributes NO facts; never copy names, numbers, dates, technologies, domains, brands, organizations, achievements, or project facts unless independently verified.
**Match the reference closely in rendering grammar; never simplify it into flat pixel graphics.**

## 5. STABLE PIXEL GRAMMAR
Required: visible medium/coarse pixel clusters; thick stepped dark outlines; complex silhouettes; multi-step shading; visible object thickness; contact/cast shadows; overlap; readable materials; local texture; secondary detail; polished high-end 16/32-bit game-illustration quality.
Reject: schematic, wireframe, flat dashboard, Figma card board, pixel-font PowerPoint, minimalist vector poster.
A flat rectangle with pixel text is NOT an illustrated object.
Do not default to night, cat, coffee, lamp, wooden desk, or city window unless evidence supports the implication.

# NARRATIVE

## 6. ROLE
`narrative` = one coherent environmental illustration, default one 1:1 image.
Goal: **build narrative meaning through one believable world.**
Build the world first; embed facts second. Do not begin from modules, cards, information trees, or panel layouts.

## 7. PLAN
Internally prepare:
```yaml
scene_proposition:
primary_world:
primary_focus:
major_metaphor:
supporting_factual_objects:
exact_text:
golden_reference:
```
Target: one coherent world; one dominant focus; one major metaphor; 2–4 supporting factual traces; few environmental connectors.
Do not maximize coverage. Do not over-minimize.

## 8. CONTENT–OBJECT BINDING
Every important object should answer: Which fact does it embody? Why is it better than another label? If removed, does meaning weaken? Without text, can its role still be partly inferred?
Prefer devices, archive drawers, tools, books, manuscripts, maps, tickets, records, status objects, storage systems, and process remnants.
Avoid turning every fact into labels, badges, floating cards, or repeated notebooks.
At least 2 supporting factual traces must exist outside the main screen.

## 9. TEXT–VISUAL BALANCE
Guiding semantic split: **~70% scene/objects/relationships; ~30% text confirmation.**
Text names, verifies, confirms status, and gives short exact tokens; it does NOT explain the whole story.
Default visible text: 10–40 Chinese characters; `generated_slogan_budget: 0`; `mode_label_visible: false`.

## 10. NARRATIVE KILL SWITCH
Reject if any is true: report board before world; central panel + side blocks dominates; no foreground/midground/background; one screen carries nearly all meaning; supporting facts are mostly labels; objects lack thickness/material/shadow; metaphor becomes more important than the real subject; materially flatter than the golden reference.
**Narrative cannot become a beautiful explanation board.**

# FACTUAL

## 11. ROLE
`factual` = illustrated report infographic, default one 1:1 image.
Goal: **quickly explain what was done, result/status, and significance.**
Modules, numbering, data, checklist, process, timeline, previews, status, and conclusions are allowed.

## 12. INFORMATION PLAN
Use 4–7 first-level modules per image. Each module must answer a DIFFERENT question.
Choose only relevant questions: `identity`, `purpose`, `structure`, `assets`, `workflow`, `changes`, `results`, `status`, `value`, `next_steps`.
Avoid differently named modules that repeat the same message. If one square cannot remain clear, paginate instead of shrinking everything.

## 13. CONTENT–OBJECT BINDING
Illustration exists to improve understanding, not to build a separate fantasy world.
At least 3 modules OR half the modules, whichever is smaller, should contain a strong semantic visual anchor: volumetric object, storage system, device, process chain, data materialization, page/device preview, status machine, or small physical vignette.
Anchors must correspond directly to module facts and must not all use the same container shape.

## 14. TEXT–VISUAL BALANCE
Guiding semantic split: **~60–70% text/titles/data/structure; ~30–40% illustration.**
Text is the information backbone. Illustration clarifies, classifies, accelerates recognition, and improves memory; it must NOT dominate the report.
Default visible text: 80–220 Chinese characters; `generated_slogan_budget: 0`; `mode_label_visible: false`.

## 15. FACTUAL RHYTHM
Vary module weight. Mix illustrated, data-heavy, process, preview, status, and concise-text modules as appropriate.
The 2–3 most important modules receive the strongest illustration budget.
Do not make every module the same size, same icon scale, same density, or same visual formula.

## 16. FACTUAL KILL SWITCH
Reject if any is true: viewer must decode a fantasy world before understanding facts; style is more memorable than content; modules become scenic islands with labels; most modules are flat boxes + icons; important facts hide behind atmosphere; hierarchy is unclear at thumbnail size; materially flatter than the golden reference.
**Factual cannot become a world-building illustration that happens to contain a report.**

# TEXT + GENERATION

## 17. COPY AUTHORITY
Allowed: verified factual text and neutral functional labels such as 项目定位 / 当前阶段 / 内容资产 / 构建链路 / 页面预览 / 后续计划.
Forbidden by default: slogans, manifesto lines, motivational summaries, AI-style philosophy, “不是……而是……”, “从……到……”.
If exact factual wording is unknown: omit it.

## 18. SHORT BRIEF ONLY
Narrative brief:
```yaml
subject:
scene_proposition:
priority_facts:
primary_world:
primary_focus:
major_metaphor:
supporting_objects:
exact_strings:
golden_reference:
aspect_ratio: 1:1
```
Factual brief:
```yaml
subject:
primary_message:
modules:
priority_visual_modules:
exact_strings:
golden_reference:
aspect_ratio: 1:1
```
Do not include this Skill, QA terms, failure history, rejected ideas, or unrelated context.

## 19. SHORT RENDERER STRING
With golden reference:
> **closely match the supplied approved reference's pixel density, outline treatment, shading depth, material richness, object dimensionality, secondary detail density, typography character, and production quality; do not simplify it into flat or minimalist pixel graphics**
Without golden reference:
> **high-detail handcrafted retro pixel illustration, visible medium/coarse pixel clusters, thick stepped outlines, rich multi-step shading, tactile materials, strong object volume, contact and cast shadows, layered depth, irregular silhouettes, dense secondary detail, polished 16/32-bit game-illustration quality**

## 20. OUTPUT ISOLATION
**ONE generation call = ONE mode = ONE standalone image.**
Generate Narrative and Factual separately. If Factual needs multiple pages, each page gets its own brief and call; all pages use identical pixel dimensions.

## 21. FIVE-POINT AUDIT
1. MODE — Narrative = coherent world? Factual = clear report?
2. REFERENCE — same visual studio as golden reference?
3. BINDING — do important objects actually embody the facts?
4. FACTS — Truth / Scope / Binding / Status pass?
5. COPY — any meta-language, unsupported text, or unsolicited slogan?
If a major failure occurs: discard, rebuild the short brief, regenerate. Do not keep stacking “do not…” clauses onto the same failed prompt.

## 22. FINAL RULE
> **Narrative owns meaning. Factual owns explanation.**  
> **Text verifies. Visuals embody.**  
> **Style serves content, never replaces it.**
