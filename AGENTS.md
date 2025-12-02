# AGENTS.md - Klisé Jekyll Blog Commands & Patterns

This document defines standard commands, workflows, and patterns for agents working on this Jekyll blog project.

## Project Overview

This is a Jekyll static site blog using the Klisé theme, customized for Jason Templeton's personal blog and portfolio. The site features light/dark mode, responsive design, and is deployed via GitHub Pages.

**Key Technologies**: Jekyll, Klisé theme, Liquid templating, SCSS, Rouge syntax highlighting

## Directory Structure

```
_posts/              # Blog posts (YYYY-MM-DD-title.md format)
_layouts/            # HTML layout templates (default, post, page, home)
_includes/           # Reusable HTML components (header, footer, navbar, etc.)
_sass/               # SCSS stylesheets (theme customization)
_data/               # Data files
assets/              # Static assets (images, CSS, JS)
_config.yml          # Jekyll configuration
```

## Development Commands

### Local Development
```bash
bundle install       # Install dependencies (run once or after Gemfile changes)
bundle exec jekyll serve    # Start local development server at localhost:4000
bundle exec jekyll build    # Build site to _site/ directory
```

### Creating Posts
```bash
# Manual: Create file in _posts/ with format YYYY-MM-DD-title.md
# Template structure:
---
layout: post
title: "Your Post Title"
date: 2024-MM-DD HH:MM:SS +0000
categories: [category1, category2]
tags: [tag1, tag2, tag3]
comments: false
---
```

### Testing
```bash
# Local testing before deployment
bundle exec jekyll serve

# Check in browser:
# - All pages load correctly
# - Light/dark mode toggle works
# - Mobile responsiveness (test at different viewport sizes)
# - RSS feed generation (/feed.xml)
# - Sitemap generation (/sitemap.xml)
```

## Common Workflows

### Adding a New Blog Post
1. Create file in `_posts/` with naming convention: `YYYY-MM-DD-title-with-hyphens.md`
2. Include proper front matter (see template above)
3. Write post content in Markdown
4. Use code blocks with language identifiers for syntax highlighting
5. Add images in post-specific folders (jekyll-postfiles plugin)
6. Include alt text for all images
7. Test locally: `bundle exec jekyll serve`
8. Commit and push to trigger GitHub Pages deployment

### Customizing Styles
1. Modify SCSS variables in `_sass/klise/_variables.scss`
2. Override color schemes for light/dark modes
3. Maintain mobile-first responsive approach
4. Test in both light and dark modes
5. Verify WCAG contrast requirements
6. Avoid inline styles - use theme's existing classes

### Updating Configuration
1. Edit `_config.yml`
2. Common changes: title, author info, URL, timezone, Google Analytics ID
3. Test locally after changes to verify no broken builds

### Deployment Verification
- Run lighthouse audit (aim for 90+ scores)
- Validate HTML with W3C validator
- Check PageSpeed Insights
- Verify sitemap and RSS feed work
- Test social media sharing
- Confirm light/dark mode works

## Styling Guidelines

### Dark Mode
- Automatic detection of system preference
- Manual toggle available in header
- Test all custom CSS in both light and dark modes
- Use SCSS variables for theming

### Responsive Design
- Mobile-first methodology (min-width media queries)
- Breakpoints defined in SCSS
- Test on mobile, tablet, and desktop viewports
- Navigation and layout adapt to screen size

### Color Palette
- Primary colors in `_sass/klise/_variables.scss`
- Maintain consistent palette across site
- Check WCAG contrast ratios for accessibility
- Override variables instead of adding inline styles

## Deployment

### GitHub Pages
- Push to repository to trigger automatic build
- Site deployed from `gh-pages` branch or configured deployment branch
- HTTPS enforced automatically
- Custom domain supported via CNAME file

### Pre-Deployment Checklist
- `bundle exec jekyll serve` runs without errors
- All pages and posts display correctly
- Light/dark mode functioning
- Mobile responsive on various devices
- HTML validates (W3C)
- Lighthouse scores 90+
- RSS feed at `/feed.xml` works
- Sitemap at `/sitemap.xml` generated

### Common Deployment Issues
- Incorrect `baseurl` in `_config.yml` causes broken links
- Missing dependencies in Gemfile breaks builds
- Timezone mismatches affect post dates
- Dark mode styles not loading (check SCSS compilation)

## Post Writing Guidelines

### Naming & Format
- Format: `YYYY-MM-DD-title-with-hyphens.md`
- Example: `2024-11-29-my-first-post.md`

### Front Matter
- `layout: post` (required)
- `title`: Keep to 50-60 characters
- `date`: Include timezone offset
- `categories`: 2-3 maximum, broad topics
- `tags`: 5-10 recommended, specific keywords
- `comments`: true/false (enable per-post)

### Content Best Practices
- Use proper heading hierarchy (##, ###, not #)
- Add alt text to all images
- Internal linking to related posts
- Optimize images before adding
- Use code syntax highlighting with language identifier

## Configuration Reference

Key settings in `_config.yml`:
- `title`: Site title
- `author.name`, `author.bio`: Profile info
- `author.github`, `author.twitter`: Social links
- `url`: Full site URL
- `timezone`: Set to America/Los_Angeles
- `mode`: Default theme ("dark" or "light")
- `google_analytics`: GA ID for tracking

## Theme Updates

```bash
# Pull updates from upstream theme
git pull https://github.com/piharpi/jekyll-klise.git

# Review changes before integrating
# Test light/dark modes after modifications
# Verify no custom styling breaks
```

## SEO & Performance

### SEO Checklist
- Descriptive post titles (50-60 chars)
- Meta descriptions where supported
- Proper heading hierarchy
- Image alt text
- Internal linking strategy
- Sitemap submitted to Google Search Console

### Performance Targets
- Lighthouse scores: 90+
- Mobile responsiveness verified
- Image optimization
- Minimize redirects
- Enable caching headers

## Plugins

The site uses these Jekyll plugins:
- `jekyll-feed`: Generates RSS feed
- `jekyll-sitemap`: Auto-generates sitemap
- `jekyll-postfiles`: Organizes post images
- `jekyll-compress-html`: Minifies HTML output

No additional plugins should be added without consideration of GitHub Pages compatibility.
