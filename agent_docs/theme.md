# Klise Theme Guidelines

## Theme Customization
- Theme uses SCSS for styling - files in `_sass/` directory
- Main configuration in `_config.yml`
- Color schemes defined in SCSS variables
- Dark mode automatically applies based on system preference or toggle

## Layout Structure
- `default.html` - Base layout wrapper
- `post.html` - Individual blog post layout
- `page.html` - Static pages layout
- `home.html` - Homepage/blog listing

## Components in `_includes/`
- `header.html` - Site header with navigation
- `footer.html` - Site footer
- `navbar.html` - Navigation bar
- Various partials for meta tags, analytics, etc.

## Customization Tips
- Override SCSS variables to change colors/spacing
- Modify layouts to adjust structure
- Add custom includes for new functionality
- Keep mobile-first approach when adding features

## Theme Updates
- Pull updates from upstream: `git pull https://github.com/piharpi/jekyll-klise.git`
- Review changes before merging
- Test light/dark modes after modifications
