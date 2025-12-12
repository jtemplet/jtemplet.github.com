# AGENTS.md

## Project Purpose

This is Jason Templeton's personal blog and portfolio, built with Jekyll and the Klisé theme. The site showcases technical writing, projects, and professional experience through a clean, performant interface with light/dark mode support.

## Technology Stack

- **Jekyll 4.x** - Static site generator
- **Klisé Theme** - Minimalist responsive theme
- **Liquid** - Templating engine
- **SCSS** - Styling with variables for theming
- **Rouge** - Syntax highlighting
- **GitHub Pages** - Deployment and hosting

## Key Directories

```
_posts/              Blog posts (YYYY-MM-DD-title.md)
_layouts/            Page templates (default, post, page, home)
_includes/           Reusable components (header, footer, navbar)
_sass/               SCSS stylesheets and variables
assets/              Images, compiled CSS, JavaScript
_config.yml          Jekyll configuration
agent_docs/          Detailed documentation for specific tasks
```

## Essential Commands

**Start development server**:
```bash
bundle exec jekyll serve
```
Serves site at `localhost:4000` with live reload.

**Build for production**:
```bash
bundle exec jekyll build
```
Generates static site in `_site/` directory.

**Verify changes locally**:
- Test at `localhost:4000`
- Check both light and dark modes
- Test mobile responsiveness
- Verify RSS feed at `/feed.xml`
- Check sitemap at `/sitemap.xml`

## Progressive Documentation

Jekyll is an in-context learner and will naturally follow existing code patterns and conventions found in the codebase. Consult these detailed guides only when relevant to your current task:

**agent_docs/building_and_testing.md**
- Development environment setup
- Build and serve commands with options
- Testing workflows and checklists
- Common build errors and solutions

**agent_docs/post_creation.md**
- Post file naming and location
- Front matter template and fields
- Markdown syntax and code blocks
- Categories, tags, and SEO practices

**agent_docs/styling_guide.md**
- SCSS architecture and variables
- Responsive design patterns
- Dark mode implementation
- Customization strategies

**agent_docs/theme_customization.md**
- Layout system and components
- Klisé theme configuration
- Adding custom features
- Theme update procedures

**agent_docs/deployment_checklist.md**
- Pre-deployment testing steps
- GitHub Pages configuration
- DNS and custom domain setup
- Performance verification

**agent_docs/seo_and_performance.md**
- On-page SEO best practices
- Core Web Vitals optimization
- Analytics setup and monitoring
- Performance testing tools

**agent_docs/troubleshooting.md**
- Build and server errors
- Content display issues
- Styling problems
- Deployment failures

## Important Notes

**Do not use agents for linting or formatting**. The project uses deterministic tools for code quality. Jekyll will naturally follow existing code patterns when provided with relevant examples from the codebase.

**Always test locally** before pushing. Run `bundle exec jekyll serve` and verify changes in the browser.

**Configuration changes require restart**. Changes to `_config.yml` only take effect after restarting the Jekyll server.
