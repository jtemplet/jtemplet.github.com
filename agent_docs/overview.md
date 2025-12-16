# Jekyll Klise Blog - Project Overview

This is a Jekyll static site blog using the Klise theme.

## Key Technologies
- Jekyll (static site generator)
- Klise theme (https://github.com/piharpi/jekyll-klise.git)
- Liquid templating
- SCSS for styling
- Rouge for syntax highlighting

## Project Structure
- `_posts/` - Blog post markdown files (YYYY-MM-DD-title.md format)
- `_layouts/` - HTML layout templates
- `_includes/` - Reusable HTML components
- `_sass/` - SCSS stylesheets
- `assets/` - Static assets (images, CSS, JS)
- `about.md` - About page content
- `_config.yml` - Jekyll configuration

## Build Commands
- `bundle exec jekyll serve` - Local development server
- `bundle exec jekyll build` - Build for production
- Site builds to `_site/` directory

## Features
- Light/Dark mode toggle
- Mobile-first responsive design
- SEO optimized
- Sitemap generation (jekyll-sitemap)
- RSS feed (jekyll-feed)
- Syntax highlighting (rouge)
- Post navigation (next/previous)
- Optional comments per post
- Google Analytics support
- HTML minification
- W3C validated markup
