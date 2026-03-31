# Agent Guide: Maciej Szwalgin Portfolio

This document provides a high-level overview for AI assistants to understand, maintain, and expand this Hugo-based portfolio project.

## 1. Project Architecture

- **Static Site Generator:** [Hugo](https://gohugo.io/) (Extended version required for Sass/SCSS processing).
- **Theme:** [Toha v4](https://github.com/hugo-toha/toha) (Managed via Hugo Modules).
- **Hybrid Dependency Management:**
  - **Hugo Modules:** Used for the theme and some core layouts (`go.mod`).
  - **NPM:** Used for frontend assets like fonts, icons (FontAwesome, Flag Icons), and utility libraries (Bootstrap, Mermaid, etc.) (`package.json`).
- **Multilingual Support:** Native Hugo multilingual features for English (`en`) and Polish (`pl`).

## 2. Content & Data Structure

### Portfolio (Landing Page)
The landing page is data-driven. Sections (About, Experience, Skills, Projects, etc.) are defined in YAML files:
- **English:** `data/en/sections/`
- **Polish:** `data/pl/sections/`
*To add or modify a section on the main page, update the corresponding `.yaml` file.*

### Blog & Technical Notes
- **Posts:** Located in `content/posts/`. Each post should be a [Page Bundle](https://gohugo.io/content-management/page-bundles/) (a folder with an `index.md`).
- **Notes:** Located in `content/notes/`. Organized by category (e.g., `bash`, `go`).
- **Multilingual Files:**
  - `index.md` -> English (Default)
  - `index.pl.md` -> Polish

## 3. Operations & Workflows

### Local Development
- **Setup:** Run `npm install` to fetch frontend assets.
- **Run Server:** `hugo server -D -E` (includes drafts and expired content).
- **Update Theme:** `hugo mod get -u github.com/hugo-toha/toha/v4`.

### Deployment
- **Platform:** Netlify (configured in `netlify.toml`).
- **CI/CD:** GitHub Actions (configured in `.github/workflows/`).
- **Automatic:** Pushes to `master` trigger a rebuild and deploy.

## 4. 2026 Strategy & Future-proofing

### Huge Pages (Performance & Large Sites)
For large-scale static sites (hundreds or thousands of pages):
- **Image Optimization:** Use Hugo's built-in [Image Processing](https://gohugo.io/content-management/image-processing/) to generate WebP/AVIF versions and responsive sizes.
- **Partial Caching:** Utilize `partialCached` in templates for components that don't change per page (e.g., navigation, footer).
- **Build Optimization:** Keep the `resources/` folder in version control or cache it in CI to speed up consecutive builds.

### AI Readability & SEO
- **Semantic HTML:** Ensure layout overrides maintain a clear header hierarchy (H1-H6).
- **Alt Text:** Always provide descriptive `alt` text in `data/` files and Markdown images.
- **Rich Snippets:** The Toha theme provides some JSON-LD; ensure `author.yaml` is fully populated to maximize "Entity" recognition by AI search engines.

### Expansion Plans (Blog & Notes)
The blog and notes features are currently **disabled** in `hugo.yaml`. To enable them:
1.  Set `params.features.blog.enable: true`
2.  Set `params.features.notes.enable: true`
3.  Add content to `content/posts/` and `content/notes/` respectively.

## 5. Directory Map (Quick Reference)

- `hugo.yaml`: Main configuration and feature toggles.
- `content/`: Markdown content (Posts, Notes).
- `data/`: YAML data for the landing page.
- `assets/`: Custom scripts and styles.
- `static/`: Publicly accessible static files (CV, images).
- `layouts/`: (If present) Custom overrides for the Toha theme.
