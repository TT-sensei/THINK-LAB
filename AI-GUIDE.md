# THINK LAB — AI GUIDE

THINK LAB is a static Japanese elementary-school thinking-tools website.

Before changing the site, read this file and README.md.

## Product purpose

Help learners make their thinking visible: expand ideas, compare information, analyze causes and relationships, organize sequences, and communicate conclusions.

The tools are for learning, not decoration. Each tool should make a thinking process easier to see and explain.

## Non-negotiable technical rules

- Use static HTML, CSS, and vanilla JavaScript.
- Do not add APIs, API keys, backend services, databases, build tools, or paid services.
- Do not add unapproved CDNs, libraries, external fonts, remote image services, or audio.
- Keep the site lightweight and tablet-first.
- Keep the core editor usable without scrolling horizontally.
- Use localStorage for optional local drafts. Explain that data stays in the current browser/device.
- Keep all controls functional. Do not add decorative or inert buttons.
- Preserve existing data keys and tool IDs when editing an existing tool.
- Keep printing available from every editor. Print styles must hide navigation, guides, and editing controls while preserving learner input.
- Use browser print for paper and PDF output; do not introduce a PDF API or service.

## Navi character rules

The Navi characters are guidance, not the main learning content.

Use the shared repository:
https://tt-sensei.github.io/navi-character-/

Before adding or changing an asset:
1. Check catalog.json for the exact character, pose, and file.
2. Prefer assets/web WebP files.
3. Do not guess filenames or paths.
4. Do not edit, copy, or repackage the master assets into this repository.
5. Do not put words, labels, or speech bubbles inside character images. Render all text in HTML.
6. Keep the character small enough that it never reduces space for the thinking tool or input fields.

There are six regular Navi characters: riku, sora, kai, saku, tsuki, nami. For ordinary guidance, choose from these characters at random; do not assign one character permanently to a subject or tool. Use the standard character poses for the meaning of the scene. Do not use fantasy costumes in ordinary thinking-tool guidance.

Shared image base:
https://tt-sensei.github.io/navi-character-/assets/web/characters/

Current shared poses confirmed across the six regular characters include:
- fullbody/waving.webp
- fullbody/hint.webp
- fullbody/correct.webp
- fullbody/retry.webp
- fullbody/complete.webp

The site currently uses waving for the home welcome and hint for tool guidance. Keep guide messages in HTML.

## Thinking tool content

Each tool should include:
- A clear name and short purpose.
- Brief steps showing how to use it.
- Examples of suitable elementary-school learning situations.
- Tips that help the learner think more deeply.
- Editable fields that match the tool's purpose.
- A print layout that remains readable with both blank and completed entries.

Do not simply add another generic text box and call it a new thinking tool. Preserve the tool's characteristic structure and make it visually distinguishable. For example, a Venn diagram must make the shared and different areas clear; a timeline must communicate temporal order; a fishbone must distinguish an outcome from its contributing causes.

Keep wording child-friendly and concise, while avoiding babyish decoration. Avoid excessive prompts that tell students exactly what to think. The tool should support the learner's thinking rather than supply the answer.

## UI principles

- Calm, modern, white/light interface with subdued blue as the main accent.
- Readable typography with system font fallbacks; no external font loading.
- Large touch targets and clear labels.
- The actual thinking area has priority over mascots and explanatory panels.
- Avoid unnecessary animation and sound.
- Support reduced-motion preferences if animation is introduced.
- Keep child-facing screens free of GitHub terminology.

## Current structure

- index.html: complete single-page application (CSS and JavaScript are inline).
- README.md: user-facing project overview.
- AI-GUIDE.md: implementation and content rules.

## Verification checklist

Before completing a change:
- Check that the HTML and JavaScript remain valid.
- Check all tool cards, search, and category filters.
- Check direct input, add/remove item actions, reset, and local save.
- Check that each tool's own guidance matches its structure.
- Check the six-character random selection and exact image paths.
- Test printing, including a blank template and filled-in content.
- Check tablet and narrow-screen layouts.
- Confirm there are no API calls, external libraries, or unapproved assets.


## Research-informed design update

The current tool library has been expanded to 30 tools. The additions include coordinate-axis sorting, diamond ranking, butterfly-style multi-perspective comparison, kumade-style perspective expansion, concentric relationship mapping, prediction planning, concept relationships, hierarchical classification, part-whole decomposition, and analogy relationships.

Design references:
- Japanese curriculum-related "thinking techniques": compare, classify, relate, sequence, and other information-processing actions.
- Japanese education-center practice materials mapping thinking skills to tools such as Venn diagrams, coordinate axes, webbing, jellyfish charts, fishbone charts, pyramid charts, and KWL.
- Project Zero's general principle that thinking routines should be selected for the type of thinking they support and used repeatedly with purpose. Do not copy Project Zero routine wording, templates, or visual materials into this site. Some individual Project Zero resources carry a CC BY-NC-ND license.
- EEF guidance on teaching planning, monitoring, and evaluating strategies in the context of curriculum learning.

Do not imply that a graphic organizer alone guarantees learning gains. The teacher should introduce, model, and revisit a tool in connection with the learning goal.

## Diagram-first layout patterns

The visual preview lives in `preview.html`; do not silently replace `index.html` before review.

Four tools have purpose-built diagram renderers in the preview:
- `mindmap`: center theme with connected branches; render `idea` and `detail` from each row.
- `webbing`: central theme with radial association nodes; render `word` and `link` from each row.
- `jellyfish`: central proposition in the dome and supporting `reason` / `example` pairs in the tentacles.
- `concept`: render each `from` / `relation` / `to` triple as a connected proposition.

Implementation constraints:
- Render learner text into the diagram using the existing `data-diag` convention so typing updates the diagram immediately.
- Read from the existing state object. Do not change the tool IDs, block/field IDs, or the localStorage schema to improve appearance.
- Escape all learner-provided text before inserting HTML.
- Keep each diagram's characteristic geometry visible; avoid replacing a diagram with generic rectangular input cards.
- Preserve blank-state hints, responsive sizing, print readability, keyboard access, and the existing add/remove actions.
- Keep Navi characters subordinate to the thinking area; never let guidance art cover or shrink the diagram.

## Second-wave diagram renderers

Keep the live preview isolated in `preview.html` until the owner reviews it. The 25 split-view tools should use individual diagram renderers; keep the diamond-ranking tool's existing non-split layout unchanged.

Purpose-built renderers added:
- `timeline`: alternating event cards anchored to a continuous vertical time axis.
- `flowchart`: numbered action nodes and optional condition notes.
- `process`: numbered action cards with a separate check/verification field.
- `cause-effect`: three stages for causes, intervening events, and results.
- `tree`: root topic, classification criterion, categories, and examples.
- `brace`: one whole on the left, decomposition brace, and component/details on the right.
- `prep`: connected Point → Reason → Example → Point sequence.
- `claim`: claim, evidence/source cards, and reasoning link.
- `reflection`: activity → learning/insight → next step.
- `brainstorm`: idea-note board.
- `imagemap` and `kumade`: radial nodes with a separate overflow list for entries beyond eight.
- `candy`: known facts/conditions → prediction/reason → verification method.
- `bridge`: A → B = C → D analogy rows with a relation label.

Maintain the exact existing block and field IDs. Every learner-editable value must have one unique `data-diag` target so the existing input listener updates the displayed diagram. Use the `dataVal` helper for escaped text and blank-state hints. Extra radial entries must provide a `data-diag` target for every field, not only the first field.

Keep the 9-position diamond ranking layout as it is in the non-split editor. It has a specific existing layout and should not be converted into the generic diagram panel without explicit approval.
