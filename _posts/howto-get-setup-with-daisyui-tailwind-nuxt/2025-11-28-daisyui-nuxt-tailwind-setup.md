---
title: How To Setup DaisyUI 5 + Nuxt 4 + Tailwind 4
date: 2025-11-26 20:58:47 +07:00
tags: [nuxt,tailwind,ui,javascript]
description: A practical guide to configuring DaisyUI 5, Nuxt 4 and Tailwind CSS 4 together as a design stack. The documentation gap for this stack which will eliminate hours of debugging. Learn the exact setup that works for production, with troubleshooting for common problems like missing component styles and theme configurations.
---

# DaisyUI + Nuxt 4 + Tailwind CSS 4: Configuration That Actually Works

When you mix DaisyUI 5, Nuxt 4, and Tailwind CSS 4, you’re working with three tools that are evolving faster than their documentation. The result is usually an hour of wondering why your buttons have no styles or why your theme refuses to load.

This guide walks through a setup that actually works in production—the exact configuration I used while building the [Orryx landing page](https://orryx.xyz).

## What You're Building

Here's the dependency chain:

1. **Tailwind CSS 4** - New architecture using CSS-first configuration (no more `tailwind.config.js`)
2. **DaisyUI 5** - Now uses Tailwind’s @plugin and CSS variables for theming
3. **Nuxt 4** - Vue framework with Vite bundler and Nitro server layer
4. **@tailwindcss/vite** - Bridge plugin that makes Tailwind work with Vite (required)

The important part: DaisyUI 5 moved most of its configuration into CSS. This is cleaner, but it’s not well documented yet.

## Project Structure

```
landing-page/
├── app/
│   ├── assets/
│   │   └── css/
│   │       └── tailwind.css         # CSS-first configuration
│   ├── components/
│   ├── pages/
│   └── app.vue                       # Apply data-theme here
├── package.json
├── nuxt.config.ts                    # Vite + Nitro config
└── tsconfig.json
```

CSS goes in `app/assets/css/`, not the project root. This matters for Nuxt's module resolution.

## Step 1: Dependencies

```json
{
  "name": "landing-page",
  "type": "module",
  "private": true,
  "scripts": {
    "build": "nuxt build",
    "dev": "nuxt dev",
    "generate": "nuxt generate",
    "preview": "nuxt preview",
    "postinstall": "nuxt prepare"
  },
  "dependencies": {
    "@tailwindcss/vite": "^4.1.16",
    "nuxt": "^4.2.0",
    "tailwindcss": "^4.1.16",
    "vue": "^3.5.22"
  },
  "devDependencies": {
    "daisyui": "^5.3.10"
  }
}
```

**Critical points:**
- Tailwind 4 requires @tailwindcss/vite
- DaisyUI should be in devDependencies
- Keep CSS inside app/assets/css for Nuxt resolution
- Use @plugin in your CSS file — not a JS config

## Step 2: Nuxt Configuration

`nuxt.config.ts`:

```typescript
import tailwindcss from "@tailwindcss/vite";

export default defineNuxtConfig({
  compatibilityDate: '2025-07-15',
  devtools: { enabled: true },

  // This imports your CSS file globally
  css: ['~/assets/css/tailwind.css'],

  // This makes Tailwind work with Vite
  vite: {
    plugins: [tailwindcss()],
  },

  nitro: {
    preset: 'aws-amplify',  // If deploying to Amplify
  },

  routeRules: {
    '/api/**': { cache: false },
  },
})
```

**What matters:**
- `css: ['~/assets/css/tailwind.css']` - Imports CSS into every page
- `vite.plugins: [tailwindcss()]` - Without this, Tailwind won't scan your templates
- `nitro.preset` - Tells Nuxt where you're deploying (affects output directory)

## Step 3: Tailwind + DaisyUI CSS

This is where everything changed in v4. Create `app/assets/css/tailwind.css`:

```css
@import "tailwindcss";
@plugin "daisyui";

@plugin "daisyui/theme" {
  name: "orryx-landing-theme";
  default: true;
  color-scheme: light;

  /* Base colors */
  --color-base-100: oklch(98.5% 0.01 60);
  --color-base-200: oklch(96% 0.015 60);
  --color-base-300: oklch(90% 0.02 60);
  --color-base-content: oklch(20% 0 0);

  /* Primary */
  --color-primary: oklch(85% 0.01 60);
  --color-primary-content: oklch(20% 0 0);

  /* Accent */
  --color-accent: oklch(74% 0.16 65);
  --color-accent-content: oklch(20% 0 0);

  /* Status colors */
  --color-info: oklch(80% 0.1 220);
  --color-success: oklch(85% 0.15 145);
  --color-warning: oklch(88% 0.15 95);
  --color-error: oklch(75% 0.15 25);
}
```

**Breaking it down:**

1. `@import "tailwindcss"` - Replaces the old `@tailwind base/components/utilities`
2. `@plugin "daisyui"` - Loads DaisyUI components
3. `@plugin "daisyui/theme"` - Defines a custom theme inline

DaisyUI 5 uses CSS custom properties in OKLch color space. Convert your hex colors with an online converter. OKLch is perceptually uniform (better than RGB/HSL).

## Step 4: Apply the Theme

In `app/app.vue`:

```vue
<template>
  <div data-theme="orryx-landing-theme">
    <NuxtPage />
  </div>
</template>
```

The `data-theme` attribute must exactly match your theme name from the CSS file. DaisyUI reads this attribute to apply the theme.

## Step 5: Use DaisyUI Components

Example component:

```vue
<template>
  <section class="bg-base-100 px-4 py-20">
    <div class="mx-auto max-w-3xl">
      <h1 class="text-4xl font-bold text-base-content">
        Your Heading
      </h1>

      <button
        class="btn btn-lg bg-accent text-accent-content hover:bg-accent/90"
      >
        Join the Waitlist
      </button>
    </div>
  </section>
</template>
```

DaisyUI classes are just Tailwind utilities. They respect your theme colors automatically via CSS variables.

## Problems You'll Hit (And How To Fix Them)

### Problem: DaisyUI classes not rendering

**Symptoms:** Buttons look unstyled, cards have no shadow.

**Root cause:** DaisyUI plugin didn't load.

**Fix:** Verify these lines exist:

In `tailwind.css`:
```css
@import "tailwindcss";
@plugin "daisyui";
```

In `nuxt.config.ts`:
```typescript
vite: {
  plugins: [tailwindcss()],
},
```

Restart the dev server after making changes.

### Problem: Theme colors are wrong

**Symptoms:** You use `btn-primary` but it's not your custom color.

**Root cause:** Theme name mismatch or theme not set as default.

**Fix:**

1. Check CSS file has `name: "orryx-landing-theme"` and `default: true`
2. Check `app.vue` has `data-theme="orryx-landing-theme"`
3. Names must match exactly (case-sensitive)

### Problem: Tailwind classes missing in components

**Symptoms:** Some Vue files have working Tailwind, others don't.

**Root cause:** Content scanning not finding your files.

**Fix:**

Tailwind 4 with `@import "tailwindcss"` auto-discovers content. If it fails:

1. Clear `.nuxt/` and `node_modules/.vite/`
2. Verify files are in `app/components/` or `app/pages/`
3. Restart dev server

### Problem: Build fails with undefined CSS variables

**Symptoms:** Build error like "Undefined variable: --color-primary"

**Root cause:** Theme plugin not parsing during build.

**Fix:**

1. Theme must be in a `.css` file imported via `nuxt.config.ts`
2. Don't put DaisyUI in a separate config file - inline it in CSS
3. Check `npm run build` output for CSS parsing errors

### Problem: Different styles in dev vs production

**Symptoms:** Works locally, wrong colors after deploy.

**Root cause:** Build output missing CSS or wrong environment.

**Fix:**

1. Run `npm run build && npm run preview` locally to test
2. Check `.output/public/` (or `.amplify-hosting/`) contains CSS files
3. Verify `nitro.preset` matches your deployment target
4. If using Amplify, ensure env vars are exported before build (see next section)

## AWS Amplify Integration

If deploying to AWS Amplify, your `amplify.yml` (in repository root):

```yaml
version: 1
applications:
  - appRoot: landing-page
    frontend:
      phases:
        preBuild:
          commands:
            - npm ci
        build:
          commands:
            - export NUXT_SUPABASE_URL="${NUXT_SUPABASE_URL}"
            - export NUXT_SUPABASE_KEY="${NUXT_SUPABASE_KEY}"
            - npm run build
      artifacts:
        baseDirectory: .amplify-hosting
        files:
          - '**/*'
      cache:
        paths:
          - node_modules/**/*
```

The `export` lines make environment variables available during build. Without them, `nuxt.config.ts` sees undefined values.

## Verification

```bash
# Development
npm run dev
# Check http://localhost:3000
# Open DevTools and inspect elements - verify DaisyUI CSS is present

# Production build
npm run build
npm run preview
# Verify styles still work

# Check output
ls -la .output/public/
# Or if using Amplify preset:
ls -la .amplify-hosting/
# Should contain index.html and _nuxt/ with CSS
```

Look at the generated CSS in `_nuxt/` - it should contain DaisyUI component definitions.

## Why This Works

1. **@tailwindcss/vite** bridges Tailwind 4 and Vite's module system
2. **CSS-first config** eliminates JS config file fragmentation
3. **@plugin directives** load DaisyUI and define themes in one file
4. **CSS custom properties** make theming dynamic without JS
5. **Nitro presets** tell Nuxt where to output for your platform

This avoids the common mistake of scattered configuration across multiple files that need to stay in sync.

## Summary

Getting this stack right:

1. Install `@tailwindcss/vite` and put DaisyUI in devDependencies
2. Import Tailwind in CSS and load it via Vite plugin in Nuxt config
3. Define DaisyUI theme in your CSS file (not in a separate config)
4. Apply theme via `data-theme` attribute in root component
5. Set `nitro.preset` if deploying to Amplify

The hardest part is understanding that DaisyUI 5 completely changed how themes work. Once you know that, the rest follows.
