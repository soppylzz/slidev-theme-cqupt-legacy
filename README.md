# slidev-theme-cqupt-legacy

> 🏊 ~~A slidev theme for cqupt students~~ **This repository has been archived.**

## ⚠️ Archived Notice

**This repository has been archived and is no longer maintained.** Please use the rewritten successor theme instead:

- New repository: [soppylzz/slidev-theme-cqupt](https://github.com/soppylzz/slidev-theme-cqupt)

The content below documents the design and usage of the legacy `slidev-theme-cqupt` (v1.0.2), kept for reference by users who still rely on the old version or need to migrate.

---

## Introduction

`slidev-theme-cqupt` is a [Slidev](https://github.com/slidevjs/slidev) theme designed for students and faculty of [Chongqing University of Posts and Telecommunications](https://www.cqupt.edu.cn/) (CQUPT). It ships with school badge/logo styling and a reusable layout & component system, commonly used for course debriefings and paper sharing. Built with Vue 3 + UnoCSS, it supports both light and dark color schemes.

## Quick Start

Specify the theme in the frontmatter of your `slides.md`. Slidev will prompt you to install it automatically on startup:

```markdown
---
theme: cqupt
---
```

Development in the current working directory:

```bash
npm install
npm run dev          # start theme preview with example.md
npm run export       # export PDF
npm run screenshot   # export PNG
```

## Layouts

| Layout | Description |
| --- | --- |
| `s-cover` | Cover page; automatically renders the `s-waist` info bar (presenters / instructors / meeting / date) |
| `s-sub-cover` | Section cover page showing the section number and school badge |
| `s-toc` | Table of contents, auto-generated from `section` entries in the frontmatter |
| `s-cols` | Multi-column content page with `col_1` / `col_2` / `col_3` slots |
| `s-vertical` | Sidebar + multi-column content layout with vertical/horizontal text and a background image (`view`) |
| `s-end` | Ending page with the school logo (`school.logo`) in the bottom-right corner |

## Components

All components use the `s-` prefix.

| Component | Description |
| --- | --- |
| `s-header` | Global header container; renders `SNav` or `SBreadcrumb` based on `header.name` |
| `s-nav` | Section navigation bar: renders each `section` and its pages (with a completed-state checkmark) |
| `s-breadcrumb` | Breadcrumb navigation (with a home icon) |
| `s-page` | Page indicator (bottom-right: `current | total`) |
| `s-waist` | Cover bottom info bar: presenters, instructors, meeting, date, etc. (with icon prefixes) |
| `s-card` | Card container supporting `header`, `icon`, and `type` (`primary` / `success` / `info` / `warning` / `danger`) |
| `s-image` | Auto-sized image with `src`, `intro` (caption), and `align` (`start` / `center` / `end`) |
| `s-align` | Alignment container, `align` × `direction` (`horizontal` / `vertical`) |
| `s-scene` | Background scene dispatcher that renders the scene matching `background.name` |

### Built-in Icons

`SiArrow`, `SiBook`, `SiCheck`, `SiHat`, `SiHome`, `SiTime`, `SiUser`

### Background Scenes

Selected via `background.name` in the frontmatter:

- `SDefault` — default decorative background images
- `SGradient` — Canvas dynamic gradient background (customizable with `colors`)
- `SPicture` — fullscreen background image (`src` + `backdrop` overlay)

## Global Frontmatter Configuration

```yaml
---
theme: cqupt
layout: s-cover

# School identity (located under public/)
school:
  badge: images/school_badge.svg
  logo: images/school_logo.svg

# Cover info bar (s-waist)
meeting: Embedded Systems Design
date: 2024-12-10
presenters: Qin He, Jiayi Li, Zhizhang Luo
instructors: Prof. Zhang

# Info bar icons and Chinese prefixes (optional)
prefixes:
  meeting:     { icon: SiBook, prefix: 课程 }
  date:        { icon: SiTime, prefix: 日期 }
  presenters:  { icon: SiUser, prefix: 汇报人 }
  instructors: { icon: SiHat,  prefix: 导师 }

# Header: SNav (section nav) or SBreadcrumb (breadcrumb)
header: { name: SNav }

# Background scene: SDefault / SGradient / SPicture
background: { name: SDefault }

# Layouts excluded from section navigation
hidden: [s-cover, s-sub-cover, s-end, s-toc, s-vertical]

# Number of entries per row in the TOC
toc: { r: 10 }

# Multi-column overflow behavior
cols: { overflow: hidden }

# Vertical layout (s-vertical)
vertical:
  view: images/view.jpg
  fromTo: ltr       # ltr | rtl
  direction: vertical
  overflow: auto    # hidden | scroll | auto

# Section marker: drives the TOC and navigation
section: Paper Introduction
---
```

## Color Variables

Theme colors are defined in `styles/vars.css` and can be overridden via CSS variables:

```css
:root {
  --s-theme: #00923f;      /* theme color (green) */
  --s-primary: #118ab2;
  --s-success: #67C23A;
  --s-info: #909399;
  --s-warning: #E6A23C;
  --s-danger: #ef476f;
  /* --s-light-1 … --s-light-8 light shades */
  /* --s-dark-1  … --s-dark-8  dark shades  */
}
```

## Directory Structure

```
layouts/     # 6 layouts
components/  # s- prefixed components
scenes/      # background scenes (SDefault / SGradient / SPicture)
icons/       # built-in SVG icons
hooks/       # useSections / useBreadcrumbs / useFrontMatter / useHidden
const/       # default config and type definitions
utils/       # utility functions
setup/       # Slidev app setup (registers global components)
styles/      # vars.css / layout.css / fonts.css
public/      # badges, logos, background images, and other static assets
```

## Requirements

- Node.js >= 18
- Slidev >= 0.50 (`@slidev/cli` ^0.50.0-beta.5)

## License

[MIT](LICENSE) © 2024 [soppylzz](https://github.com/soppylzz)
