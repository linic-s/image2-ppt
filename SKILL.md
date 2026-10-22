---
name: image2-ppt
description: Create presentations from source materials and a topic through an image-first workflow. Generate three visual samples for user selection, generate complete slide images one at a time, reconstruct each image as an editable PowerPoint slide, add native animations, and deliver the deck and ordered images. Use for image2-ppt or requests for this style-selection and image-to-PPT workflow; ordinary text-only deck edits do not require it.
---

# image2-ppt

Follow this sequence: **materials and topic → three visual samples → user selection → all slide images, one by one → PPT reconstruction, one by one → animation and delivery.**

Match the user's language. Start a new project unless continuing existing work. Do not inherit a previous project's facts, colors, or page count as universal defaults.

## Tools

- Read the installed `imagegen` skill before image production. Use its built-in image generation tool by default. “image2”, “imagen2”, and “imagenskill” refer to the intended image-generation stage, not a guaranteed tool name or exposed model parameter. Do not invent tool names or claim a specific model when the tool does not expose one.
- If a user requires a particular model, verify that it is selectable before proceeding. Follow imagegen's rules for CLI/API fallback; never silently switch or request an API key for the built-in route.
- Read the installed `presentations` skill before PPT authoring. Call `load_workspace_dependencies` to locate runtimes and follow current authoring, rendering, and export requirements.
- The installed `ppt-master` skill can support reconstruction or native animation. When using it, resolve its registered path, read its entrypoint, and follow its integrity check and selected route. Do not copy its implementation or load unrelated routes.
- Resolve skill paths from the session catalog; do not hardcode usernames, plugin versions, or undocumented commands.

## 1. Establish content

Read supplied materials and relevant prior work before asking for information. Accept papers, data, notes, existing decks, images, or a topic alone. Ask only for missing information that materially determines the result. Otherwise state reasonable assumptions for audience, use, length, and aspect ratio (16:9 by default).

Save an ordered content plan with each page's purpose, exact title, visible copy, chart values, source location, and intended layout. Reuse an agreed outline. Show a concise outline with the style samples; add a separate outline approval only if the user asks for one.

For quantitative work, calculate counts and percentages from evidence before prompting for images. Specify denominators, units, labels, rounding, and category order. Never let an image model invent chart values. Explain findings in concrete language, with deeper interpretation where useful. Do not invent studies, quotations, tests, or observed behavior, or present interpretation as measured evidence.

## 2. Produce three visual samples and obtain a choice

Use imagegen to create exactly three distinct design directions unless the user specifies another number. Vary composition, typography, palette, and visual treatment, rather than only background color.

Use the **same representative page and exact content** across the samples so the user can compare designs fairly. Prefer a content-rich page when the deck includes substantial text or charts. Each sample must be one complete slide with readable text, not an empty background or a collage of multiple slides.

Save and display separate samples A, B, and C, each with a brief design description. Ask the user to select a style. **Wait for an explicit selection before producing the full image set.** A previous selection or instruction to match a reference satisfies this gate; do not ask again. A sample revision request does not approve full production.

Record the selected image path and style specification: canvas, palette, typography hierarchy, margins, decoration, chart styling, and text density. Pass the selected image as a style reference in later image calls. Inspect local reference images first, following the imagegen contract.

## 3. Generate every slide image sequentially

Generate page 01, inspect and save it, then proceed to page 02. Use one call per slide, with focused retries for flawed pages. Do not parallelize page generation or generate several pages in one stitched image.

Each prompt includes one full slide at the chosen aspect ratio, the selected visual reference, fixed style specification, page purpose and composition, exact visible text, and exact data labels. Request consistent identity with layout adapted to the page. Exclude device frames and mockup perspective.

Images must contain the intended text. Keep content substantial and readable through explanations and evidence rather than tiny type. Choose chart types appropriate to the data; do not use a bar chart on every page.

Inspect each result for text, numbers, chart geometry, clipping, and consistent style. Correct defects with the supported image-editing workflow or regenerate that page. After two unsuccessful focused corrections of the same critical defect, report the concrete issue and seek direction rather than silently marking it complete. Verified programmatic charts may be supplied as supporting references where precise geometry matters.

Save accepted pages as `images/01_short-title.png`, `images/02_short-title.png`, etc. Preserve the actual image format; do not rename bytes to a different extension. Save prompts and source-to-page mappings.

**Finish and inspect all requested slide images before PPT reconstruction.** No second batch approval is needed unless requested. If the user requests images only, deliver them and stop here.

## 4. Reconstruct each image as a PPT slide

Read [references/reconstruction-and-motion.md](references/reconstruction-and-motion.md) at this stage.

Process images in numeric order, one image to one slide. Use the accepted image as visual authority and the content plan as text/data authority. Default to editable text, supported native charts, and separate logical elements; retain complex artwork as images.

Match proportions, spacing, colors, and line breaks closely. Do not quietly substitute a full-slide screenshot for editable reconstruction. Honor an explicit request for an image-only deck with the corresponding animation approach in the reference.

Render each reconstructed page and compare it with its image before advancing. Repair missing or duplicate text, changed values, chart distortions, overlaps, and material layout drift. Mark the page complete only after this check.

## 5. Animate and deliver

After reconstruction of all pages, add restrained native PowerPoint animations following the reference. Invoking this workflow already requests animation; do not ask for permission again. Do not add narration, music, video, or automatic slide advancement unless requested.

Validate page order, dimensions, content, editability, and animation targets. Render every slide and repair defects. Verify slideshow playback when available. Never claim playback was tested using static thumbnails alone.

Deliver the final animated `.pptx`, individually numbered slide images in an ordered folder (ZIP when useful or requested), and editable content plan, style specification, prompts, and actual PPT authoring source or reconstruction project.

Save to the user's requested destination when permitted; otherwise use the task output folder and provide links. State material editability or animation limitations briefly. Do not mark incomplete requested stages as completed.

## Continuity

Maintain a small `manifest.json` with topic, sources, page count, selected style, phase, and each page's image path, PPT index, checks, and animation status. Update after successful saves. Store no secrets.

On continuation, verify manifest paths and resume the first unfinished stage. When content or style changes, invalidate only affected pages and dependent PPT/animation artifacts. Preserve source files and earlier deliveries.
