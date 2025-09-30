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

### Project Structure

```
src/
├── layouts/
│   └── BaseLayout.astro       # Main layout with <html>, <head>, <body>
├── components/
│   ├── Navigation.astro        # Site navigation (accepts currentPath prop)
│   └── Footer.astro            # Site footer
├── pages/
│   ├── index.astro             # Homepage
│   ├── about.astro             # About page
│   └── contact.astro           # Contact page
└── styles/
    └── global.css              # Global styles and CSS variables
```

### Layout System

The site uses a single base layout (`src/layouts/BaseLayout.astro`) that:
- Accepts `title` and `description` props for SEO
- Imports and applies global styles from `src/styles/global.css`
- Includes Navigation and Footer components
- Uses `<slot />` for page-specific content
- Automatically passes current path to Navigation for active link styling

### Routing

File-based routing where pages in `src/pages/` map directly to routes:
- `src/pages/index.astro` → `/`
- `src/pages/about.astro` → `/about`
- `src/pages/contact.astro` → `/contact`

### Styling Architecture

**Global Styles** (`src/styles/global.css`):
- CSS custom properties (design tokens) in `:root`
- Base reset and body styles
- Shared component styles (navigation, footer, buttons)
- Imported once in BaseLayout, available to all pages

**Design Tokens**:
- `--primary: #1e40af` (blue)
- `--primary-dark: #1e3a8a`
- `--secondary: #059669` (green)
- Gray scale from `--gray-50` to `--gray-900`
- `--max-width: 1200px` for content containers

**Page-Specific Styles**:
- Each page has a `<style>` block for page-specific layouts and sections
- Styles are scoped by default in Astro
- Use semantic class names (`.hero`, `.features`, `.contact-section`)

### Common UI Patterns

**Navigation Component**:
- Accepts `currentPath` prop to highlight active page
- Uses `.active` class for current page styling
- Global styles in `src/styles/global.css`

**Hero Sections**:
- Homepage: `.hero` with gradient background and larger padding (6rem)
- Secondary pages: `.hero-small` with solid background and smaller padding (4rem)

**Buttons** (defined in global.css):
- `.btn-primary` - Blue background, white text, hover effect
- `.btn-secondary` - White background, blue border and text

**Content Sections**:
- Consistent padding of `4rem 2rem` (vertical, horizontal)
- Alternating backgrounds (white and `var(--gray-50)`)
- Centered content with `max-width: var(--max-width)`

**Responsive Design**:
- Mobile breakpoint at `@media (max-width: 768px)`
- Navigation gap reduces on mobile
- Typography scales down appropriately

## Creating New Pages

1. Create a new `.astro` file in `src/pages/`
2. Import and wrap content in `BaseLayout`
3. Pass `title` and `description` props
4. Add page-specific styles in a `<style>` block
5. Use CSS variables from global.css for consistency

Example:
```astro
---
import BaseLayout from '../layouts/BaseLayout.astro';
---

<BaseLayout
  title="Page Title"
  description="Page description for SEO"
>
  <section class="my-section">
    <!-- Page content -->
  </section>
</BaseLayout>

<style>
  .my-section {
    padding: 4rem 2rem;
    /* Use CSS variables like var(--primary) */
  }
</style>
```

## Configuration

- TypeScript config extends `astro/tsconfigs/strict`
- Astro config is minimal with no integrations
- No build tools or preprocessors beyond Astro's defaults
