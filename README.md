# BMC Jekyll Website

BobbyMcGlone Circuit Designs — Electronic Consulting

## Quick start

```bash
gem install bundler jekyll
bundle install
bundle exec jekyll serve
```

Then open `http://localhost:4000` in your browser.

---

## Project structure

```
bmc-jekyll/
├── _config.yml          # Site configuration
├── _layouts/
│   ├── default.html     # Base layout (nav + footer)
│   ├── post.html        # Blog post layout
│   └── project.html     # Portfolio project layout
├── _includes/
│   ├── nav.html         # Navigation bar
│   └── footer.html      # Footer
├── _posts/              # Blog posts (YYYY-MM-DD-title.md)
├── _portfolio/          # Portfolio projects
├── assets/
│   ├── css/main.css     # All styles
│   └── images/          # Logo and project images
├── index.html           # Home page
├── portfolio/index.html # Portfolio listing
├── blog/index.html      # Blog listing
└── contact/index.html   # Contact page
```

---

## Adding a blog post

Create a new file in `_posts/` named `YYYY-MM-DD-your-title.md`:

```markdown
---
title: Your Post Title
date: 2025-06-01
read_time: 5 min read
tags: [PCB Design, Firmware]
excerpt: One sentence summary shown in the blog listing.
---

Your post content in Markdown here.
```

---

## Adding a portfolio project

Create a new file in `_portfolio/` named `project-slug.md`:

```markdown
---
title: Project Name
category: PCB Design
date: 2025-06-01
tech: STM32 · 4-layer
image: /assets/images/projects/my-project.jpg   # optional
specs:
  - label: MCU
    value: STM32F4
  - label: Year
    value: "2025"
---

Project description in Markdown here.
```

Add any project images to `assets/images/projects/`.

---

## Setting up the contact form

The contact form uses a standard HTML `<form>` POST. Replace `ACTION_URL` in `contact/index.html` with your [Formspree](https://formspree.io) endpoint:

```html
<form action="https://formspree.io/f/yourcode" method="POST">
```

Sign up free at formspree.io — no backend code needed.

---

## Hosting (free options)

- **GitHub Pages** — push to a repo, enable Pages in settings. Free and automatic.
- **Netlify** — drag and drop the `_site/` folder after `bundle exec jekyll build`, or connect your Git repo.
- **Cloudflare Pages** — connect your Git repo, set build command to `jekyll build` and output directory to `_site`.
