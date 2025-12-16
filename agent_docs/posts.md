# Blog Posts Guidelines

## Post Location
All blog posts go in `_posts/` directory

## Naming Convention
Format: `YYYY-MM-DD-title-with-hyphens.md`
Example: `2024-11-29-my-first-post.md`

## Front Matter Template
```yaml
---
layout: post
title: "Your Post Title"
date: 2024-11-29 10:00:00 +0000
categories: [category1, category2]
tags: [tag1, tag2, tag3]
image: /path/to/featured-image.jpg  # Optional
comments: true  # Enable comments for this post
---
```

## Writing Posts
- Use Markdown syntax
- Front matter is required
- Images organized with jekyll-postfiles plugin
- Syntax highlighting with triple backticks and language identifier
- Use proper heading hierarchy (##, ###, etc.)

## Post Images
- Store in post-specific folders when using jekyll-postfiles
- Reference with relative paths
- Include alt text for accessibility
- Optimize images before adding

## Categories vs Tags
- Categories: Broad topics (2-3 max)
- Tags: Specific keywords (5-10 recommended)
- Both help with navigation and SEO

## SEO Best Practices
- Write descriptive titles (50-60 characters)
- Include meta description in front matter if supported
- Use headings appropriately
- Add alt text to images
- Internal linking to related posts
