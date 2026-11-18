---
name: "exam-solution"
description: "Turn a past exam paper into an HTML replica with the answers handwritten in place (or a clean unsolved copy), plus a PDF. Use when asked to solve a past exam, make an exam solutions sheet, or a clean copy of an exam."
---

# Exam solution

Build one self-contained HTML file per exam that looks like the exam paper itself, with every answer written in place in handwriting, as if a student solved the paper, plus a PDF of it. Several exams means several separate HTML files and PDFs, named as the user asks.

Section 7 (Taste) holds the author's style defaults. Follow them unless the user asks for something else.

## 1. Gather and verify

1. Read the exam paper and every lecture file it covers. Scanned PDFs and screenshots: read them as images.
2. Note each question's number, points and exact wording, plus the paper's header (university, course, model, date, time, number of questions, full points). Transcribe scanned papers into clean text (zoom into blurry parts); keep the paper's numbering even if a number is missing or cut off, and tell the user in chat which readings were unclear or missing.
3. **Check scope.** Search the slides for each question's terms. Answer every question anyway, and tell the user in chat which ones are not in the slides. Only if the user says the exam covers just some lectures, color out-of-scope questions red with a ✗ after the number, leave them unanswered, and add a one-line red legend under the header.
4. **Compute every answer in code**: counts, traces, expected outputs, table values, matrix and modular arithmetic, anything with a definite value. Use only verified values. Compile and run any code you write as an answer. If the slides or the user's answer key disagree, follow the key on the page and explain the disagreement in chat, never on the page.
5. Solve with the method the slides teach. If the slides don't cover a step, use the simplest standard method and mention in chat that it is not in the slides.

## 2. Answer style

- **Answers go where the student would write them:** blanks filled, table cells filled, the chosen radio circle or checkbox filled in the handwriting color, drawings in the answer space, code on the dotted answer lines. No separate SOLUTION block under the question.
- **Short and only what the question asks.** No asides, no working the question doesn't ask for (a full trace when only the final value is asked), no restating a filled table in words. Write what earns the marks, nothing more.
- **Explanation notes** in the same handwriting, one or two short lines under a part, only where the marks need working (a count, why a choice is the only valid one) or the user asks for explanations.
- **Assumptions:** answer with the most likely reading and explain the assumption in chat, not on the page. Add a one-line handwritten note only if the user asks for it.
- **No matching option:** if the computed value matches no MCQ option, write the value and fill the closest option.
- **Check-all questions:** fill the circles of the true statements. **True/False questions:** write `( True )` or `( False )` after each statement as the paper lays it out; only false statements get a one-line handwritten correction, and only if the paper asks for one.
- **Tables the question asks for** are drawn as handwritten tables: borders and text in the handwriting color.
- **Drawings** (graphs, state diagrams, trees, circuits) go in a bordered answer box, drawn with strokes in the handwriting color and handwritten labels.
- **Never align columns with spaces** in handwriting: the font is proportional, so columns drift. Use a handwritten table, one item per line, or `|` separators.
- **Grids that are part of the work** (a key matrix, a lookup table) are drawn plain and centered in the answer space, with no "Given" box and no side notes.
- **Timing and scheduling answers** (latency, throughput, cycle counts, process schedules) are drawn as a small Gantt chart, one bar per item on a time axis.
- **Simplest correct method.** Prefer the shortest argument (e.g. prove the property for one step or one case that generalizes, instead of tracing indices through every step).
- **Proofs and calculations:** one step per handwritten line, each substitution with a short reason in brackets, the general formula before numbers, the final answer on its own line (e.g. `Answer: 42`).
- **"Explain" and "differentiate" questions:** one or two handwritten lines per item, with the term first (`Term A: ...`, `Term B: ...`).
- **Use the student's notation** when they give their own attempt; correct it rather than replacing it.

## 3. Page layout: replicate the paper

- **Match the paper's look and structure**, from the paper or the screenshots the user gives: its font family (a typewriter-style paper uses a monospace font such as Fira Mono), header block, question numbering (`1.`, `(a)`), boxed point labels (`[1 point]`, `[2 pts.]`), horizontal rules between questions, bold stems where the paper has them, bullets, radio circles for MCQ options, underlined blanks, dotted answer lines, and tables with the paper's borders (e.g. a double rule between two halves).
- **Code listings** look like the paper's: line numbers outside the box in small gray, a light box with a thin border, and the paper's syntax colors; a plain bordered box if the paper's code is plain.
- No section headings, no gray question boxes, no `Q<n>` label column, no SOLUTION labels: the paper's own structure is the structure. Only add a short centered "Solution" line under the header.
- **Handwriting:** a handwriting font with unambiguous digits, in one blue, slightly larger than the print in blanks and cells.
- **Dotted answer lines** are real elements, one `div` per line with `border-bottom: dotted`. Never draw ruled lines with CSS gradients: some mobile viewers render them as a pink fill.
- Escape `<` and `&` in SVG text (a raw `i<a` breaks the drawing).
- No interactive tools. KaTeX only if the paper has typeset math; otherwise write `2<sup>3</sup>`.
- Check in headless Chromium (Playwright) at 1280, 390 and 320px: no horizontal scroll, fonts loaded. Wrap every table and code box in an `overflow-x:auto` container with `position:relative`, and on phones let the question body stretch (`align-items: stretch`) so wide code or tables scroll inside instead of widening the page.

## 4. Unsolved copy and question images

- **Unsolved copy:** the same replica with no handwriting: empty blanks, empty circles, empty `(     )`, empty dotted lines. Title it as the user asks; make it a separate HTML file and PDF.
- **Combining question screenshots** into one PDF: place them in order on A4 pages (reportlab), scaled to the page width with small gaps, as many per page as fit.

## 5. Build and deliver

1. **Write one self-contained HTML file.** Inline all CSS, JS and fonts (fonts as data URIs) so it opens offline and renders the same in the PDF. Get the fonts with `npm pack` from `@fontsource/*` (the paper's font and the handwriting font, latin subset, only the weights used), and `katex@0.16.9` if the paper has typeset math. If an asset can't be fetched, link it from a CDN instead and tell the user the file needs internet for it.
2. **Export the PDF** in the format Taste sets. Wait for `document.fonts.ready` first.
   - **One tall page, A4 wide:** viewport 794px, `emulate_media('screen')`, inject `@page{size:auto;margin:0}`, measure `scrollHeight` as `h`, then `page.pdf(width='210mm', height=f'{h+2}px', print_background=True, margin=0)`. PDF pages cannot exceed about 200 inches: if `h` is over about 18,500px, pass `scale = 18500 / h` and shrink width and height by the same factor.
   - **A4 pages:** `pdf(format='A4', print_background=True)` with `break-inside: avoid` on each question.
   - Check `pdfinfo` reports the expected page count, `pdffonts` shows the handwriting font, and look at a rendered preview of every part.
3. **Name the files as the user asked** and deliver them: send them if the environment has a file-sending tool, otherwise save them to the output folder and give the paths. After every later edit, regenerate both files and deliver them again.
4. **Reply in chat** with unclear readings, out-of-scope questions, assumptions made, and any disagreement with the slides or the answer key.

## 6. Feedback

Apply each point the user raises, regenerate the HTML and the PDF, deliver them again, and reply in one or two lines in the user's language. When feedback points at a pattern (a note, a box, a verbose step), fix every place on the page where it occurs and say so. "Remove if not required" means: keep only what the question asks for. Feedback that only asks a question gets an answer, not a page change.

## 7. Taste

The author's defaults. Follow them unless the user asks otherwise.

- Handwriting font: Kalam (clear digits; Caveat's 7 looks like a question mark), color `#1f4fd8`.
- PDF: one tall page, A4 wide, by default; A4 pages only when the user asks for printable pages.
- No em dashes anywhere.
- No page meta (nothing written about the page itself) and no source attribution ("from the slides", "as the professor said").