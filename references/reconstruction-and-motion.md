# Reconstruction and native motion

Read after the full accepted image set exists. Use current tool documentation for API syntax.

## Editable reconstruction

1. Match image and deck aspect ratios. Inventory title, body, data, artwork, and logical reveal groups.
2. Use exact content-plan text and chart values. OCR can locate elements but does not override source copy or numbers.
3. Build editable textboxes and supported native charts using available fonts. Reconstruct chart geometry from data rather than estimating values from pixels.
4. Keep complex illustrations as image assets, with clean background or separate artwork layers as needed. Use the available image-editing tool to remove raster text when reconstructing editable text over artwork. Do not put a full rendered page beneath duplicate editable labels: it causes ghost text and exposes content before the animation.
5. Group elements by meaningful unit, such as one finding or a diagram stage. Record stable object IDs for animation targeting. Preserve native chart data; a raster chart is not editable.
6. Compare a same-size rendered slide with the reference: hierarchy, alignment, crop, contrast, words, and numeric labels. Do not promise pixel-identical editable rendering across all Office applications.

Retain a difficult illustration as one animatable image rather than degrading the entire page to a screenshot. If the whole page must remain raster, disclose the limitation and obtain the user's choice before substituting for editable output.

## Animation

Use native PowerPoint object animations in addition to any page transitions. A page fade alone does not satisfy content animation on an editable deck.

- Keep title and background visible initially.
- Reveal content groups in reading or argument order, usually 2–4 groups on a dense page.
- Prefer appearance or fade, about 0.3–0.5 seconds; use a directional wipe when it explains a process.
- Default to click-triggered reveals for presenter control. Leave decoration static.
- Keep chart labels with corresponding series. Avoid intermediate states with misleading denominators, axes, or totals.
- Reveal interpretation after its supporting evidence when helpful.
- Use restrained page fades around 0.4 seconds. Keep page advancement on click unless self-running playback is requested.

For an explicitly image-only deck, the full-slide image is one animatable object. Whole-image entrance and page transitions are feasible. Individual text or chart reveals require separate reconstruction or clean layers. Do not label transitions as object-level animation.

Prefer documented native animation support in the installed tooling. If using `ppt-master`, enter its applicable route and use its documented configuration and validation. Do not invent unsupported API flags or timing XML from memory.

If the active exporter lacks animations, use an available documented PowerPoint/OOXML mechanism after export, then revalidate the actual final file. If none is available, preserve the usable deck and images and state that animation remains unfinished. Never deliver a static deck as completed animation work.

## Verification

- One slide per image in numeric order, no duplicate or missing page.
- Inspect editable objects and chart data, not only rendered appearance.
- Animation targets point to existing objects on the correct page, including after merging/export.
- Initial and final visibility states are coherent; essential text is not permanently hidden.
- Check playback in a suitable app when available; static images cannot verify timing or click behavior.
- Validate the final animated file after animation processing, not only the earlier static draft.
