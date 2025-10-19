# Project website (Jekyll + GitHub Pages)

This repository hosts a static website built with Jekyll and deployed to GitHub Pages. It includes structured content data, a projects/gallery section, and a contact form powered by Formspree.

If you are setting up the project locally or contributing changes, follow the steps below.


## Prerequisites

- Ruby 3.x installed (rbenv, asdf, or system Ruby)
- Bundler and Jekyll gems
- Git
- Optional: Node.js (if you add any JS tooling) and ImageMagick or Squoosh/Sharp for image optimization

Install the Ruby gems globally (or let Bundler manage them per project):

```bash
gem install bundler jekyll
```


## Local development

1. Install dependencies

   ```bash
   bundle install
   ```

2. Serve locally with live reload

   ```bash
   bundle exec jekyll serve
   # Site will be available at http://127.0.0.1:4000 (or the port Jekyll prints)
   ```

3. Build for production (optional)

   ```bash
   JEKYLL_ENV=production bundle exec jekyll build
   # Output will be generated in the _site/ directory
   ```

Notes:
- If you encounter missing gems, run `bundle install` again.
- If you change `_config.yml`, restart `jekyll serve` to see config updates.


## Project structure (conventions)

This repo follows common Jekyll conventions. Not all folders may be present yet, but when added they should align with the structure below:

```
/
├─ _config.yml            # Site configuration (title, url, baseurl, plugins, etc.)
├─ _data/                 # YAML/JSON/TOML data files (site content, navigation, projects index)
├─ _includes/             # Reusable partials
├─ _layouts/              # Page/post layouts
├─ _pages/ or pages/      # Top-level pages (about, contact, etc.)
├─ _projects/             # Collection for projects (each project as a Markdown file)
├─ assets/ or _assets/    # CSS, JS, fonts, etc.
├─ images/                # Images and media assets
├─ index.md / index.html  # Homepage
└─ _site/                 # Build output (ignored by git)
```


## Configuration

Most site-wide settings live in `_config.yml`. Common keys you may see or add:

```yaml
title: Your Site Title
description: Short description for SEO
url: https://your-username.github.io  # or your custom domain
baseurl: /your-repo-name              # project sites only (omit for user/org pages)

# Contact / Formspree
formspree:
  form_id: "<your-formspree-form-id>"

# Collections
collections:
  projects:
    output: true
    permalink: /projects/:slug/

# Defaults (example front matter defaults)
defaults:
  - scope: { path: "_projects", type: "projects" }
    values: { layout: project }
```

If the project prefers centralizing editable content in data files, you may also find or create `_data/content.yml` (or `_data/projects.yml`, `_data/navigation.yml`, etc.).


## Updating the Formspree ID

The contact form uses Formspree for submissions.

1. Create or sign in to Formspree and create a form.
2. Copy the Form ID (it looks like `xyzzabcd` or similar).
3. Update the ID in `_config.yml` under `formspree.form_id`, or wherever the template expects it (some sites use `_data/settings.yml` or `_data/site.yml`).
4. If the contact page hardcodes the form endpoint in its front matter or HTML, update it there. The action typically looks like:
   ```html
   <form action="https://formspree.io/f/<your-form-id>" method="POST">
   ```
5. Redeploy the site. Submit a test message to verify delivery.

Tip: Do not commit personal email addresses; Formspree hides them. Use environment variables for secrets if you add any build-time integrations.


## Editing content data

- Site-wide content such as navigation, footer links, social profiles, or a list of projects can be stored under `_data/` as YAML.
- Example: `_data/projects.yml`

  ```yaml
  - title: Example Project
    summary: One sentence about the project.
    thumbnail: /images/example-thumb.png
    hero: /images/example-hero.png
    tags: [ruby, jekyll]
    external_url: https://example.com
    repo_url: https://github.com/org/example
  ```

If you use a projects collection instead of `_data/projects.yml`, create a file per project in `_projects/` with front matter:

```markdown
---
layout: project
title: "Example Project"
date: 2024-01-01
summary: "Short summary for cards and meta."
tags: [ruby, jekyll]
thumbnail: /images/example-thumb.png
hero: /images/example-hero.png
external_url: https://example.com
repo_url: https://github.com/org/example
---

Longer project description, screenshots, and details go here.
```


## Adding new projects and assets

- Prefer one Markdown file per project in `_projects/` (or an entry in `_data/projects.yml` if your templates are data-driven).
- Images go in `images/` (organize by topic, and use kebab-case names: `project-name-hero.png`).
- Optimize images before committing:
  - Convert large photographic images to WebP when possible
  - Target widths: 400px (thumb), 800px, 1600px (hero)
  - Use `loading="lazy"` for below-the-fold images
- Keep alt text meaningful and concise; see accessibility notes below.


## Accessibility best practices

- Use semantic HTML: headings in order (h1 → h2 → h3), landmark regions (header, nav, main, footer).
- Provide descriptive alt text for images; omit alt or use empty alt only for purely decorative images.
- Ensure strong color contrast (WCAG AA). Test hover/focus states too.
- All interactive elements must be keyboard-accessible and have visible focus styles.
- Label all form controls; associate labels via `for` and `id`.
- Avoid using ARIA if semantic HTML already conveys the meaning; when needed, use ARIA correctly.
- Use descriptive link text (avoid “click here”).


## Performance best practices

- Optimize and compress images; prefer modern formats (WebP/AVIF) with PNG/SVG for graphics.
- Provide responsive images (`srcset`/`sizes`) for large visuals.
- Minimize JavaScript; avoid render-blocking scripts/styles.
- Inline critical CSS only if necessary; otherwise keep CSS small and cacheable.
- Use `JEKYLL_ENV=production` to enable production builds and minification (if configured via plugins/pipelines).


## Deployment (GitHub Pages)

There are two common ways to deploy with GitHub Pages:

1) Build on GitHub Pages (simple)
- In your repository: Settings → Pages
- Source: `main` (or `gh-pages`) branch, `/ (root)` directory
- GitHub Pages will build with the supported Jekyll version
- Ensure `_config.yml` does not require unsupported plugins

2) Build via GitHub Actions (flexible / Jekyll 4+)
- Use a Jekyll build-and-deploy workflow to build the site and publish the `_site/` output to the `gh-pages` branch
- Keep `url` and `baseurl` in `_config.yml` accurate:
  - User/org site: `url: https://<user>.github.io` and omit `baseurl`
  - Project site: `url: https://<user>.github.io` and `baseurl: /<repo>`
- For custom domains, add a `CNAME` file and set your DNS records; update `url` accordingly

After deployment, test:
- Pages render correctly at the expected path (watch for `baseurl` issues)
- Contact form submissions reach Formspree
- Images and assets load over HTTPS without mixed content


## Contributing

- Create a feature branch from the default branch.
- For documentation-only updates, prefix your branch with `docs/` (e.g., `docs/readme-tweaks`).
- Write clear, descriptive commit messages.
- Verify locally with `bundle exec jekyll serve` before opening a pull request.
- Pull requests should include screenshots or links for UI changes when possible.

If this repository adopts a Code of Conduct or CONTRIBUTING guide later, follow those documents.


## License

If a `LICENSE` file is present in the repository, its terms apply to all source and content here. If no license is specified, the repository is private by default and all rights are reserved by the maintainers. Contact the maintainers for reuse permissions.


## Troubleshooting

- Error: “You must use Bundler X or greater with this lockfile” → Upgrade bundler: `gem install bundler`.
- GitHub Pages doesn’t reflect changes → Ensure you committed your changes and that Pages is pointed at the correct branch/folder; if using Actions, confirm the workflow ran successfully.
- Styles/scripts not loading at the deployed URL → Check `url` and `baseurl` settings in `_config.yml` and asset paths in templates.
