# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AllHats is a landing page for an AI-powered command center for delivery managers. It's a **single-file static site** (`index.html`) with no build system, no dependencies, and no framework.

## Development

Open `index.html` directly in a browser. No server or build step required.

## Architecture

Everything lives in one `index.html` file:

- **CSS** — Inline `<style>` block using CSS custom properties for dark/light theming (`[data-theme="dark"]` / `[data-theme="light"]`). Design system uses heavily abbreviated class names (e.g., `.bf` = button filled, `.bo` = button outlined, `.bc` = bento card, `.pf` = preview frame).
- **HTML** — Static marketing content: nav, hero, integration logos (inline SVGs), app preview mockup, "how it works" steps, feature bento grid, testimonials, waitlist CTA, footer.
- **JS** — Inline `<script>` at bottom:
  - Theme toggle with `localStorage` persistence (key: `ah`)
  - Canvas background animation: constellation nodes + floating UI fragment shapes (cards, kanban boards, charts, etc.)
  - `IntersectionObserver` for scroll-reveal animations (`.rv`/`.rs` classes)
  - Waitlist form handler (currently just logs to console)

## Key Conventions

- CSS variables are defined on `:root` and theme-switched via `[data-theme]` attribute selectors
- Class names are ultra-short (1-3 chars) — refer to the CSS for meaning
- Canvas colors are read from CSS custom properties (`--cd`, `--cl`, `--cg`, `--cp`, `--cf-stroke`, `--cf-fill`) so the animation respects theme changes
- Responsive breakpoints: 900px (hides sidebar/panel in preview, single-col bento) and 768px (hides nav links, single-col steps)
