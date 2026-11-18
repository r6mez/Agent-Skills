---
name: "study-summary"
description: "Turn a lecture's notes, slides or code (often handwritten scans) into a self-contained interactive HTML study page and PDF for exam prep. Use when asked to summarize or explain a lecture for studying."
---

# Study summary

Build one self-contained HTML study page, plus a PDF of it, that teaches a lecture to a reader who **did not attend and did not read the lecture**. The page is their only source, so every term, symbol and number must be explained on the page before it is used.

Section 8 (Taste) holds the author's style defaults. Follow them unless the user asks for something else.

## 1. Gather and verify

1. Read every page of the lecture files. Scanned or handwritten PDFs have no text layer, so read them as images.
2. Write down: the concepts taught, every worked question (verbatim, including any hints written under it), all given numbers, the lecture's code, and anything the professor said about the exam.
3. **Run the lecture's code and recompute every worked number**, installing whatever it needs (prefer CPU-only or lightweight builds). Handwritten arithmetic on slides is sometimes wrong. Use the verified value on the page and tell the user about the discrepancy in your reply.
4. If the exam asks for something the lecture's code doesn't print directly (an intermediate output, a count, a trace), write the extra code to produce it and copy the real output into the page.
5. If past exams or quizzes are provided, note which topic each question tests, and tell the user in your reply which questions fall outside the lectures being covered.

## 2. Plan the structure from the content

There is no fixed section order. Design the structure that best teaches this material, in the order a reader can follow it without knowing anything yet. The list below is a set of ingredients, not a template; use the ones the content needs, where they fit.

- **Several lectures on one page: one part per lecture, in lecture order.** Each part teaches its lecture completely (its concepts, its worked questions, its code) before the next part starts. Later parts build on earlier ones and say only what changes. Never regroup several lectures by kind (all concepts, then all questions, then all code), because the reader then meets material from lectures they have not reached yet.
- **No up-front glossary and no up-front overview of everything.** Do not open with a table of terms or a big-picture diagram covering material the reader has not met. Define each term in the sentence where it is first needed. A diagram goes in the part where its subject is first taught.
- **Each lecture part opens with a short "What this lecture is about" block**: the problem the lecture solves and its two or three parts in order. This is per lecture, not an overview of the whole page.
- **Within a lecture, follow the lecture's own logic**, usually: why the idea is needed, the idea, a worked question as soon as the reader has what it needs, then the code that implements it, with anything the exam asks about that code placed right after it.
- **Code:** the full lecture code, placed in the part it belongs to, plus notes on only the non-obvious lines.
- **Exam recipes:** if the exam needs a procedure (a count, a trace, a derivation), teach each formula where its concept is introduced; a short closing recipe can then gather the steps without re-deriving them.
- **Past-exam and quiz questions** that belong to a topic stay inside that topic, folded under "Show answer".
- **Exam-prep length.** When several lectures go on one page for an exam, keep each topic short: one sentence of why it exists, then the definition in close to the slides' wording, then the formula and its example. A page nearly as long as the slides is too long. Drop detail that no past exam touches and that only describes the internals of one specific product or tool, unless the user wants it.
- **Cheat sheet:** a table of "You need" and "Use" at the very end, where a compact summary of terms is fine because the reader has now met them all.

**Before writing, check the plan: could a reader who reads top to bottom understand each section using only what came before it? If not, reorder.**

## 3. Writing rules

- **Reason first, in plain prose, briefly.** Each concept opens with one or two sentences on why it is needed, in natural words, then what it is and how it helps. Never jump straight to a definition or a conclusion. Some topics (a dataset, a tool) have no problem to state; just say what it is and what it is used for.
- **Show real code, not descriptions of code.** When a concept involves code, show the actual lecture lines as a code block (the full loop, every line of a definition) with short end-of-line comments. Never replace code with a sentence summarizing it, and never list fragments separated by commas.
- **Compare code as code.** To show two ways of writing the same thing, use one short code block per style, not a table that splits the syntax across rows.
- **Name exactly what a formula computes.** The left side states the precise quantity ("worst-case number of comparisons", not "cost" or "size"). Define symbols just as precisely.
- **Write the general formula before plugging in numbers.**
- **Define before use, and only at the point of use.** Every symbol is defined in a short list *above* the formula or table that uses it, never below it. Every new term is explained where it is first needed. Every acronym is spelled out at first use. Leave out tool, library and product names the exam doesn't need; keep only the one example the slides rely on and say what it is.
- **Explain each idea once.** If a concept already explains why a step exists, the worked solution only calculates. No why/how explanations repeated in solutions or exam sections.
- **Worked question layout.** A **Question** block with the question as the lecture states it and its hints on separate lines, exactly as written. Then a **Given** block with all the given data shown as grids, vectors or tables. Then a **Solution** with numbered steps that only calculate. For every exam or past-exam question, put the Given and the Solution inside a collapsed `<details>` with the summary "Show answer", so the reader can try first, and style every answer fold as a framed box clearly separate from the content below it. If the solution relies on settings that are in neither the question nor the hints, state where each one comes from (a diagram, the code).
- **Simplest correct method, matched to the slides.** For proofs and derivations, use the shortest argument that answers the question (e.g. prove the property for one step or one case that generalizes, instead of tracing indices through every step). Don't add textbook material the slides don't cover, and give one example per idea, not extra larger ones.
- **Interpret the result plainly.** Say what the final number means in plain words, including how confident or close it is.
- **Parallel items go in bullets, not one paragraph.** When a paragraph or a table cell defines, contrasts or lists two or more parallel things (A vs B, two requirements, several design choices), write a short lead-in, then one bullet per item with the term in bold (`<b>Term</b>: meaning`). This applies inside table cells too. Use a numbered list when the items are ordered or counted. Keep the shared conclusion as its own sentence after the list. Before finishing, scan every paragraph and table cell for this pattern.
- **Mark past-exam topics.** When past exams or quizzes are provided, put a small `past exam` badge after each definition or concept that one of them asked about.
- **Match the professor's other material.** If an exercise sheet uses different symbols than the slides, show the mapping next to the formula. If exercises solve a formula backwards (an input from a target output), teach the rearranged formulas too.
- **Ambiguous exam questions.** When a question leaves an assumption open, give the most likely answer with the assumption in one line and the alternative result in one line.
- **Comparing a family of related methods** (any set of techniques, algorithms, models or criteria the lecture lists side by side) uses one table:
  - the abbreviation beside every full name the first time, then the abbreviation everywhere after;
  - a column phrased as the exact question or goal each method addresses;
  - one shared minimal example worked by every method, written in the simplest abstract form (symbols or T/F values rather than code with concrete numbers), so the rows differ only in the method;
  - a column with the general formula or cost where one exists (count, complexity, minimum size), with its symbols defined above the table.
  Every cell states its content explicitly: never "both of the above", "X and Y together" or "X plus...". Say what it does, then name the relation in brackets ("(both X and Y)"). Don't add explanation bullets under a table; the table must carry the comparison itself.
- **Don't over-explain the lecture's code.** Show it with its comments; add notes only for lines that are genuinely confusing.
- **Exam sections are direct.** Say how to do it (a conversion table, a recipe), not why other approaches fail.
- **Skip what earlier lectures taught.** If study pages for earlier lectures are provided or exist in the working folder, read them first and do not re-explain their concepts; refer to them in a line at most.

## 4. Visuals

- **If the text describes something visual, draw it right there.** Never describe a diagram, a structure, a flow, a curve or a shape in words alone. This covers every figure the lecture itself draws and every idea that has a natural picture: data flowing between stages, state passed from one step to the next, a quantity growing or shrinking over steps, two curves compared, a baseline vs an actual series, a function's shape. Put the diagram next to the sentence that talks about it, and write the sentence to read the diagram ("on the left...", "the top line is..."). Before finishing, scan the page for words like diagram, loop, line, flows, curve, shape, passes, connects; each one needs a drawing.
- **LaTeX for all math and numbers in prose** (dimensions, formulas, results), rendered with KaTeX auto-render.
- **Show a mapping with colors and one worked example, never a web of lines.** For any mapping (items to slots, keys to buckets), color each item by where it may go, list which items each slot accepts, and walk one concrete sequence step by step in each variant (place A, place B, use A again). Many crossing arrows explain nothing.
- **Highlight consistently.** If one diagram in a family colors its key path, color the matching path in its siblings too.
- **One small visual example per case.** When a method has several cases, put a small diagram with a worked example under each case, input highlighted in one color and output in another, with a one-line caption.
- **No calculators or "try it" tools** that redo a procedure the page already works by hand; a static highlighted example teaches better.
- **Interactive where it teaches.** For example, clicking a result highlights the inputs that produced it and shows the computation behind it.
- **Visualize dimensions.** When data has three or more dimensions (stacks, layers), draw it in isometric SVG and show how it unrolls when flattened. Color-code where values came from. A 3D block must always look 3D: draw the front, top and side faces, even when one dimension is 1. Never draw a 3D shape as a flat grid.
- **Grids for matrices**, with negatives highlighted. Show before/after for each operation.
- **Syntax-highlight code** with Prism. Keep printed program output plain.

## 5. Layout rules

- **Center diagrams and size tables to their data.** Tables use `width: auto` and `margin: auto`, never stretched to the full width. Rows of grids and pipelines use `justify-content: safe center`. SVGs are centered with `margin: auto` and `width: 100%`, capped at `max-width: min(calc(var(--w) * 1.3), 1100px)` with `--w` set to their natural width, so they never blow up on a wide screen.
- **Prose gets a readable width, visuals don't.** Paragraphs, lists, definition lists and notes get `max-width` of about 60rem. Diagrams, matrix rows, tables and code are never width-limited: a row of grids forming one equation stays on one line on desktop.
- **Text wraps cleanly.** Set `text-wrap: pretty` on `p, li, dd, td, figcaption`. After KaTeX renders, add `white-space: nowrap` to each inline `.katex` narrower than `min(220px, 40vw)`; longer inline math may wrap. Don't end a sentence on a short formula right before a figure; move the formula earlier in the sentence.
- **Phones.** No sideways scroll at 390px or 320px, and nothing squeezed: grid cells, boxes and labels keep their natural size (`flex-shrink: 0` on items in a row of grids, `white-space: nowrap` in cells). A row of grids that sits on one line on desktop wraps onto several lines under `@media (max-width: 600px)`. Give `position: relative` to every scroll container (table wrappers, `pre`, formula boxes, `li`, `td`), otherwise KaTeX's hidden MathML escapes it and the whole page scrolls sideways. Tables placed side by side in a flex row get `flex-shrink: 1; min-width: 0; max-width: 100%`.
- No SVG text in fixed-width boxes (it overflows); use HTML blocks that wrap. Escape `<` and `&` in SVG text.

## 6. Build and deliver

1. **Write one self-contained HTML file.** Inline all CSS, JS and fonts (fonts as data URIs) so it opens offline and renders the same in the PDF. Get the assets with `npm pack`: `katex@0.16.9` (CSS, woff2 fonts, `katex.min.js`, auto-render), `prismjs` (core plus the languages used), and the page fonts from `@fontsource/*` (only the weights used). If an asset can't be fetched, link it from cdnjs instead and tell the user the page needs internet for it.
2. **Check it in headless Chromium** (Playwright): no KaTeX errors, no raw `$` left in the text, no horizontal scroll at 320px and 390px, no lone token on the last line of paragraphs at 390, 800 and 1280px. Take a screenshot of the densest section and look at it.
3. **Export the PDF** in the format Taste sets. Before exporting, open every `<details>`, hide interactive buttons and wait for `document.fonts.ready`.
   - **One tall page:** viewport 794px, `emulate_media('screen')`, inject `@page{size:auto;margin:0}`, measure `scrollHeight` as `h`, then `pdf(width='210mm', height=f'{h}px', print_background=True)`. PDF pages cannot exceed about 200 inches: if `h` is over about 18,500px, pass `scale = 18500 / h` and shrink width and height by the same factor. Check `pdfinfo` reports 1 page.
   - **A4 pages:** `emulate_media('print')`, then `pdf(format='A4', print_background=True)`. Look at the pages for empty pages or headings separated from their content.
4. **Name both files after the page title** (e.g. `Lecture 3 - Hashing.html` and `.pdf`). Deliver them: send them if the environment has a file-sending tool, otherwise save them to the output folder and give the paths.
5. **Reply** with what the page covers, any corrections to the lecture's numbers, and any past-exam questions outside the covered lectures.

## 7. Handling feedback

The user points at parts of the page (quoted text, a screenshot, a description). For each point: make the change, regenerate the HTML and the PDF, deliver them again, and say in one line what changed, in the language the user wrote in.

- When feedback says a part is unclear ("explain the differences more", "I can't tell them apart"), restructure that part (usually into the comparison table above), don't only explain it in chat.
- If feedback only asks a question ("why this +1?"), answer it in chat and **do not add the answer to the page** unless the user asks. If the question shows a label is vague, fix only that wording.
- When feedback points out a pattern problem (a format, code described instead of shown), fix every place on the page where it occurs, not just the one pointed at, and say so.

## 8. Taste

The author's defaults. Follow them unless the user asks otherwise.

**Content**
- No em dashes anywhere.
- The page opens with its title only: no subtitle, no orientation sentence, and no word like "Mid" or "Exam" in the title.
- No question banks on the study page: practice problems, drills, True/False sets, MCQ sets and past-exam answer keys go in separate files, made only when asked. A practice file has a one-line instruction, a defaults box, a short title and the code for each problem; its answer table shows the working for every column, then one "Watch out" line naming the trap.
- No labelled rows like Problem / Fix / Code; write prose.
- No page meta: never write about the page itself ("this page assumes...", "this section covers", "see section 03"). Only teach.
- No source attribution ("the lecture's diagram", "the professor's example"). Present the material directly. Lecture numbers are fine as part titles and for cross-references ("as in Lecture 4").
- Corrections, slide errors and trap notes go in the chat reply, never on the page.
- PDF: one continuous tall page by default; A4 pages only when the user asks for printable pages.

**Page style: colored printable paper**
- Full-width white page: the white background fills the whole window (no grey surround, no fixed-width sheet), with side padding like `clamp(16px, 5vw, 72px)`. Light theme only, no dark mode.
- Serif throughout (Source Serif 4) for headings and body; IBM Plex Mono only for code and grid cells.
- Rules, not boxes: headings get a thin rule underneath, numbered "01." style. Concepts are separated by thin lines with no background. Only the Question and Given boxes are framed, with a light blue fill.
- Colors by role. Blue accent (`#1f4fbf`, soft `#e5ecfb`) for section numbers, the header rule, table headers, highlighted grid cells, inputs in worked examples, buttons and bars; key formulas use the blue soft fill with a blue left rule. Orange-red (`#b5490f`, soft `#fbeee4`) for negatives, outputs in worked examples and the `past exam` badge; notes use the orange soft fill with an orange left rule.
- Answer folds: 1px border, a 4px blue left rule, a light fill, padding, and a thin rule under the summary when open.
- Square corners on grids, buttons, boxes and bars. Grid labels in italic serif.
- Print CSS: `@page { size: A4; margin: 16mm 15mm; }`; `print-color-adjust: exact` so colors print; switch `main`, sections and blocks to `display: block` in print (grid layouts fragment badly); `break-inside: avoid` on blocks, steps, tables, code and formula boxes; `break-after: avoid` on headings; hide interactive buttons; open every `<details>` on `beforeprint`; let code wrap.