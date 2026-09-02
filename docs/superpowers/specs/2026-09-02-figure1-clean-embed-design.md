# Figure 1 Clean Embed Design

## Goal

Provide a clean Notion embed entrypoint for Figure 1 that shows only the chart, with no page header, explanatory copy, or figure caption.

## Visual behavior

- Keep the existing Figure 1 SVG, data, smoothing, colors, annotation, and hover tooltip behavior unchanged.
- Hide the masthead, all figures after Figure 1, and the colophon in the embed entrypoint.
- Hide the Figure 1 title, subtitle, and `figcaption`; the chart frame is the only visible content.
- Increase chart-internal text (axis ticks, axis label, and annotation) to approximately 1.3x the current size.
- Preserve responsive width and the existing light/dark color behavior.

## Implementation boundary

Only `figure1.html` changes. The full `index.html` page remains available for the complete figure set. No data, chart geometry, or interaction logic changes are required.

## Verification

- Load the public Figure 1 URL and confirm only the chart frame is visible.
- Confirm no title, subtitle, caption, or other figure sections appear.
- Confirm enlarged axis and annotation text remains inside the chart frame at desktop and narrow widths.
- Confirm hover tooltip still appears over the chart.

