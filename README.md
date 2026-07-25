# maciejszwalgin.github.io

## My personal portfolio

Made using Hugo and Toha theme.

## Local Development

To run this project locally, follow these steps:

1.  **Install Node.js Dependencies:**
    ```bash
    npm install
    ```

2.  **Start the Hugo Development Server:**
    ```bash
    hugo server -D -E
    ```

3.  **Access the Site:**
    The site will be available at [http://localhost:1313](http://localhost:1313).

### Prerequisites

- [Hugo (Extended version)](https://gohugo.io/installation/) — must be installed and added to your system `PATH`
- [Node.js](https://nodejs.org/)

## Updating Hugo & the Toha Theme

1.  **Update the Hugo binary:**
    Download the latest **extended** release from the [Hugo releases page](https://github.com/gohugoio/hugo/releases) (file name contains `extended`, e.g. `hugo_extended_X.Y.Z_windows-amd64.zip`) and replace your existing `hugo` executable. Verify with:
    ```bash
    hugo version
    ```
    The output must include `+extended` — the Toha theme requires it to compile SCSS/Sass.

2.  **Sync the pinned Hugo version in CI/CD** so builds match your local version:
    - `.github/workflows/merge-to-main.yml`, `pull-request.yml`, `theme-update.yml` — field `hugo-version`

3.  **Update the Toha theme module:**
    ```bash
    hugo mod get -u github.com/hugo-toha/toha/v4
    ```

4.  **Regenerate `package.json`** from the theme's declared npm dependencies:
    ```bash
    hugo mod npm pack
    npm install
    ```

5.  **Verify the build:**
    ```bash
    hugo mod tidy
    hugo server -D -E
    ```
    Check that the site builds without errors or unexpected deprecation warnings, and that the pages render correctly (especially the data-driven sections under `data/en` and `data/pl`).

6.  Commit `go.mod`, `go.sum`, `package.json`, `package-lock.json` together.
