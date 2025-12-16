# Deployment Guidelines

## Build Process
1. Run `bundle exec jekyll build`
2. Output goes to `_site/` directory
3. HTML is automatically minified
4. All assets compiled and optimized

## GitHub Pages
- Push to `gh-pages` branch or configure in repo settings
- Jekyll builds automatically on push
- Custom domains supported via CNAME file
- HTTPS enforced by default

## Testing Before Deploy
- Run `bundle exec jekyll serve` locally
- Test all pages and posts
- Verify light/dark mode
- Check mobile responsiveness
- Validate HTML (W3C validator)
- Run Lighthouse audit
- Test RSS feed and sitemap

## Configuration
- Set proper `url` and `baseurl` in `_config.yml`
- Update Google Analytics ID if used
- Configure RSS feed settings
- Set timezone appropriately

## Performance Checks
- Lighthouse scores (aim for 90+)
- PageSpeed Insights
- Image optimization
- Minimize redirects
- Enable caching headers

## SEO Verification
- Submit sitemap to Google Search Console
- Verify RSS feed functionality
- Check meta tags on all pages
- Test social media sharing
- Validate structured data if present

## Common Issues
- Incorrect baseurl causes broken links
- Missing dependencies in Gemfile
- Timezone mismatches affect post dates
- Dark mode styles not loading
