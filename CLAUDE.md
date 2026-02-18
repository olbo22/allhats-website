# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

AllHats landing page — a single-file static site (`index.html`) for an AI-powered delivery management command center. Content reflects the product concept from `allhats-konzept-v5_5.md` (in the main allhats repo).

## Development

Open `index.html` directly in a browser. No server or build step required.

## Architecture

Everything lives in one `index.html` file:

- **CSS** — Inline `<style>` block using CSS custom properties for dark/light theming (`[data-theme="dark"]` / `[data-theme="light"]`). Design system uses heavily abbreviated class names (e.g., `.bf` = button filled, `.bo` = button outlined, `.bc` = bento card, `.pf` = preview frame).
- **HTML** — Marketing content: nav, hero, integration logos (inline SVGs), app preview mockup (showing spec pipeline + AI chat), "how it works" (5 phases: Context, Ideation, Planning, Execution, Quality), feature bento grid, testimonials, waitlist CTA, footer.
- **JS** — Inline `<script>` at bottom:
  - Theme toggle with `localStorage` persistence (key: `ah`) and `aria-pressed` state
  - Canvas background animation: constellation nodes + floating UI fragment shapes — pauses when tab is hidden via Page Visibility API
  - `IntersectionObserver` for scroll-reveal animations (`.rv`/`.rs` classes)
  - Waitlist form connected to Supabase (`waitlist` table)

## External Dependencies

- **Supabase JS** via CDN — for waitlist form submissions
- **Google Fonts** — Sora typeface

## Supabase Waitlist

The form inserts into a `waitlist` table on the AllHats Supabase instance. SQL to create:

```sql
CREATE TABLE IF NOT EXISTS waitlist (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  email TEXT NOT NULL UNIQUE,
  created_at TIMESTAMPTZ DEFAULT now()
);
ALTER TABLE waitlist ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Allow anonymous inserts" ON waitlist FOR INSERT WITH CHECK (true);
```

## Key Conventions

- CSS variables are defined on `:root` and theme-switched via `[data-theme]` attribute selectors
- Class names are ultra-short (1-3 chars) — refer to the CSS for meaning
- Canvas colors are read from CSS custom properties (`--cd`, `--cl`, `--cg`, `--cp`, `--cf-stroke`, `--cf-fill`) so the animation respects theme changes
- Responsive breakpoints: 900px (hides epic sidebar in preview, single-col bento) and 768px (hides nav links, single-col steps)
- Content language: English
