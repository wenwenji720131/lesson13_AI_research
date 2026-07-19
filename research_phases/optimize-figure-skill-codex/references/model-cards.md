# Model Cards

Use these cards as execution adaptation. Do not let model preferences override scientific facts, domain style, or figure-type constraints.

## Default Priority

1. **Nano Banana Pro**: default model for final-candidate academic figures, complex multi-zone diagrams, strict arrows, and stable redraws.
2. **gpt-image-2**: use when text-rich system diagrams, many labels, or clear editable structural drafts matter more than visual richness.
3. **Nano Banana 2**: use only when the user asks for fast candidate exploration or multiple versions. Still produce a high-quality academic prompt, not a rough-sketch prompt.

## Nano Banana Pro

Best for publication-quality scientific illustrations with complex structure.

Adaptation:
- Use explicit multi-zone layout, module positions, hierarchy, arrow semantics, and visible-text whitelist.
- Ask for high-fidelity academic figure style, refined low-saturation palette, strong composition, clean labels, and final-candidate quality.
- Add strict negative constraints: no casual sketch, no simple flowchart, no decorative icons, no layout drift.

## Nano Banana 2

Best for rapid alternatives when the user wants several candidate directions.

Adaptation:
- Keep zones and module names very explicit.
- Warn that internal structure words such as `ZONE`, `LAYOUT`, and `CONNECTIONS` are prompt instructions, not visible labels.
- Reduce label count if the figure becomes crowded, but do not collapse scientific structure.

## gpt-image-2

Best for text-rich architecture diagrams, system figures, and clean redraw bases.

Adaptation:
- Allow richer controlled labels and short phrases when they clarify workflow.
- Make geometry, arrows, ordering, and module boundaries precise.
- Prefer clean vector-like academic style, white background, restrained colors, and readable typography.

## Compare Mode

When the user asks for all three prompts, output three independent prompts with the same scientific structure but model-specific rendering constraints. Order them by recommended quality path: Nano Banana Pro, gpt-image-2, Nano Banana 2.
