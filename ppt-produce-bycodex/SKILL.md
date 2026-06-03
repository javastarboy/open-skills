---
name: ppt-produce-bycodex
description: Create and iterate enterprise application software solution PPTs as full-page PNG slides and optional PPTX decks. Use when the user wants to start, design, generate, redraw, repair, batch-produce, or package a business/consulting/enterprise software solution presentation, especially with imagegen/gpt-image-2, PPT PNG pages, contact sheets, or PPTX assembly.
---

# PPT Produce by Codex

Use this skill to run a disciplined enterprise-solution PPT production workflow: clarify project context, create a storyline and page plan, generate full-page PNG slides with `imagegen`/`gpt-image-2`, review quality, and assemble PPTX only when useful.

For the complete reusable playbook, read `references/ppt-production-guide.md` when planning or executing a real deck. Keep this `SKILL.md` as the quick operating procedure.

## Required Intake

Before creating files or generating slides, confirm these fields. If any are missing and cannot be inferred from the current workspace, ask the user for them first.

- Project name
- Project root directory
- Solution topic or PPT title
- Target audience or customer type
- Current output version, such as `v1`, `v2`, or `v3`
- Desired deliverables: PNG only, PPTX, outline MD, scheme MD, contact sheet, demo prototype, or a subset
- Available source materials: meeting notes, docs, screenshots, old PPT, reference images, brand assets, existing outline

If the user gives a project root, keep all new artifacts under `<project-root>/workspace/`. Do not create root-level `output/`, `outputs/`, `tmp/`, or `scripts/` folders.

## Default Workspace Layout

Use this layout unless the project already has a compatible convention:

- `workspace/deliverables/` for final outputs
- `workspace/assets/` for reusable source assets and copied references
- `workspace/runs/` for generation batches, staging outputs, backups, and contact sheets
- `workspace/tmp/` for temporary prompts, OCR, unpacked PPTX checks, and scratch scripts
- `workspace/scripts/` for reusable generation and verification scripts

Report full absolute paths for every created or modified file.

## Workflow

1. Inspect current files and existing versions. If a higher version directory exists than the user mentioned, ask which version is authoritative.
2. Collect missing intake fields before generating.
3. Read `references/ppt-production-guide.md` for detailed guardrails.
4. Build or update the PPT storyline: background, positioning, overall architecture, core capabilities, scenarios, value, implementation path.
5. Create a page plan with page title, page type, visible text, source assets, and generation method.
6. Generate 2-4 sample pages before batching when a visual direction is not yet approved.
7. Use small batches, staging folders, and contact sheets. Do not overwrite approved PNGs without a backup.
8. Only assemble PPTX when the user asks or after a meaningful batch is confirmed; otherwise ask whether to generate PPTX.
9. If business content changes, sync the scheme MD / PPT outline / PNG page content so future delivery and demos stay consistent.

## Image Generation Rules

When generating or redrawing PPT PNG pages:

- Use the `imagegen` skill at `/Users/javastarboy/.codex/skills/.system/imagegen/SKILL.md`.
- Use `gpt-image-2` unless the user specifies another image model.
- Check `OPENAI_API_KEY` and `OPENAI_BASE_URL` from `~/.zshrc`, then call `/models` before expensive batches.
- Do not use low quality.
- Use at least `2048x1152 high` for normal 16:9 slides.
- Use native `3840x2160 high` for complex architecture, dense diagrams, or key customer-facing pages.
- Never upscale a local 2K image into 4K and call it final.
- Final pages must be full-page PNGs. Do not build final visual content with local HTML/CSS/Canvas/PPT elements.
- Do not render fixed page numbers, watermarks, prompt labels, task requirements, internal notes, or draft labels.

If a model returns unexpectedly small images below 2K without user permission, stop batch generation and warn that the provider/model route may be degraded.

If the same repair task returns `response too large` three times via different attempts, stop and create a handoff prompt instead of retrying indefinitely.

## Local Repair Rules

For local fixes such as removing page numbers, repairing text, or changing a small region:

- Use `gpt-image-2 image edit` based on the source image.
- Do not cover bad regions with local translucent masks, solid blocks, pasted text, or screenshots.
- Repair the needed region with the model, then composite only that region back into the source.
- Verify dimensions, RGB/opaque output, no residual old text, and pixel-identical unchanged regions.
- Stage outputs under `workspace/runs/<task>/` or `workspace/tmp/<task>/`; overwrite final PNG only after review.

For title-style repairs, use a cropped title-header reference instead of a whole slide reference, to avoid reference-slide content leaking into the target page.

## Prompt Discipline

Separate visible slide text from design instructions.

Use this prompt shape:

```text
STRICT VISIBLE TEXT ONLY:
customer-visible short phrases only.

DESIGN BRIEF - DO NOT RENDER AS TEXT:
fragmented design instructions.

LAYOUT BRIEF - DO NOT RENDER AS TEXT:
layout and hierarchy.

VISUAL STYLE - DO NOT RENDER AS TEXT:
color, texture, title style.

CONTENT EMPHASIS - DO NOT RENDER AS TEXT:
business meaning to emphasize.

FORBIDDEN VISIBLE TEXT:
describe categories of forbidden text; avoid repeating long forbidden phrases.
```

Never let the slide show prompt field names, task wording, internal discussion, review notes, or "this page should..." language.

## Visual Direction

Default to a premium enterprise/internet style:

- Light background, blue-white base
- Small accents in gold, orange, teal/green, or purple
- Clean, credible, restrained, technical but not flashy
- Unified left-aligned content-page title system
- Large readable diagrams/screenshots on image-heavy pages

Avoid cyber neon, heavy dark backgrounds, strong glow, cheap 3D stacks, one-note blue/purple gradients, dense grid backgrounds, oversized titles, and template-like layouts.

## PPTX Policy

PPTX is a packaging artifact. It should contain only one full-slide PNG per page.

Do not rebuild PPTX after every small PNG change. For ongoing page edits, generate PNGs and contact sheets first, then ask whether to build PPTX.

When building PPTX, verify:

- Slide count and order
- One full-page picture per slide
- No local text boxes, shapes, notes, page numbers, or placeholder remnants

## Useful Script

Use `scripts/check_png_assets.py <png-dir>` to inspect PNG dimensions, mode, and alpha. This is a quick check only; still visually inspect contact sheets and key pages.
