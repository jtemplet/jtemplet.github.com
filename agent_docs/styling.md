# Styling Guidelines

## SCSS Structure
- Theme uses Sass/SCSS for styling
- Files located in `_sass/` directory
- Compiled automatically by Jekyll
- Variables centralized for easy customization

## Responsive Design
- Mobile-first approach (min-width media queries)
- Breakpoints defined in SCSS variables
- Test on mobile, tablet, and desktop
- Navigation adapts to screen size

## Dark Mode
- Automatic detection of system preference
- Manual toggle available
- Color variables for both themes
- Test all custom styles in both modes

## Customization Approach
1. Override SCSS variables first
2. Add custom classes sparingly
3. Maintain mobile-first methodology
4. Keep accessibility in mind (contrast ratios)
5. Test dark mode after changes

## Color Customization
- Primary colors in `_sass/klise/_variables.scss`
- Dark mode colors in same file
- Maintain consistent color palette
- Check WCAG contrast requirements

## Typography
- Font stacks defined in variables
- Responsive font sizes
- Line height for readability
- Proper heading hierarchy

## Performance
- Minified CSS in production
- Avoid inline styles
- Use theme's existing classes when possible
- Optimize custom CSS
