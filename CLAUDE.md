# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Astro-based static website for Public Works Digital, a company focused on building open-source government technology. The site uses minimal dependencies and is built with Astro 5.14.1.

## Development Commands

All commands run from the project root:

- `npm run dev` - Start development server at localhost:4321
- `npm run build` - Build production site to ./dist/
- `npm run preview` - Preview production build locally
- `npm run astro ...` - Run Astro CLI commands (e.g., `npm run astro check`)

## Architecture

### Page Structure

This is a file-based routing system where pages in `src/pages/` map directly to routes:
- `src/pages/index.astro` → `/` (homepage)
- `src/pages/about.astro` → `/about`
- `src/pages/contact.astro` → `/contact`

### Styling Approach

Each `.astro` file contains its own scoped `<style>` block. Styles are NOT shared across pages. The project uses:
- CSS custom properties (CSS variables) defined in `:root` for theming
- Consistent design tokens across all pages:
  - `--primary: #1e40af` (blue)
  - `--primary-dark: #1e3a8a`
  - `--secondary: #059669` (green)
  - Gray scale from `--gray-50` to `--gray-900`
  - `--max-width: 1200px` for content containers

When adding styles to a page, follow this pattern:
1. Define shared variables in `:root`
2. Use semantic class names (`.hero`, `.features`, `.contact-section`)
3. Include mobile responsive breakpoints at `@media (max-width: 768px)`

### Common UI Patterns

**Navigation**: Each page includes identical nav markup with sticky positioning. The active page link uses the `.active` class.

**Hero sections**:
- Homepage uses `.hero` with larger padding (6rem) and gradient background
- Secondary pages use `.hero-small` with smaller padding (4rem) and solid gray background

**Buttons**: Two button styles available:
- `.btn-primary` - Blue background, white text
- `.btn-secondary` - White background, blue border and text

**Content sections**: Use consistent padding of `4rem 2rem` (vertical, horizontal) with alternating background colors (white and `var(--gray-50)`)

## Configuration

- TypeScript config extends `astro/tsconfigs/strict`
- Astro config is minimal with no integrations
- No build tools or preprocessors beyond Astro's defaults
