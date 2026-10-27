# MyST Website Template

A reusable template for building websites with [MyST Markdown](https://mystmd.org/) and automated deployment via GitHub Actions.

## Features

- **MyST Markdown** source format with Jupyter notebook integration
- **GitHub Pages** deployment on push to `main`
- **Netlify PR previews** for pull request review
- **Pre-commit hooks**: Black, codespell, nbstripout for code quality

## Quick Start

1. Click **Use this template** on GitHub to create a new repository
2. Update `myst.yml` with your site title, author, and table of contents
3. Replace placeholder content in `pages/` with your own pages
4. Push to GitHub to trigger automated builds

## Project Structure

```
.
├── myst.yml                    # MyST configuration
├── index.md                    # Landing page
├── requirements.txt            # Python dependencies
├── logo.png                    # Site logo
├── fav.ico                     # Favicon
├── CNAME                       # Custom domain (optional)
├── robots.txt                  # Search engine directives
├── pages/                      # Site content
│   ├── preface.md
│   ├── part01/
│   │   ├── getting-started.md
│   │   └── installation.md
│   ├── part02/
│   │   └── first-example.md
│   ├── references.bib          # Bibliography
│   ├── jupytext.toml
│   └── images/                 # Shared images
├── .pre-commit-config.yaml     # Pre-commit hook configuration
├── CONTRIBUTING.md              # Contribution guidelines
├── CONDUCT.md                   # Code of conduct
└── .github/workflows/
    ├── build.yml               # PR preview builds (Netlify)
    └── deploy.yml              # Production deployment (GitHub Pages)
```

## Customization

### Site Metadata

Edit `myst.yml`:
- `project.title`: your site title
- `project.authors`: author name(s)
- `project.github`: your GitHub `username/repo`
- `project.toc`: table of contents structure

### Adding Pages

1. Create a new `.md` file in the appropriate `pages/` subdirectory
2. Add the file to `project.toc` in `myst.yml`

## Building Locally

```bash
pip install -r requirements.txt
npm install -g mystmd
myst build --html
```

The built site will be in `_build/html/`.

## Deployment

### GitHub Pages (production)

Pushes to `main` automatically trigger the `deploy.yml` workflow, which builds the HTML site and deploys to GitHub Pages.

By default, `BASE_URL` is set to `/<repo-name>` so that asset paths work correctly when served at `username.github.io/repo-name/`. If you configure a custom domain (via `CNAME`), remove the `BASE_URL` environment variable from `deploy.yml` since the site will be served from the root.

### Netlify (PR previews)

Pull requests trigger the `build.yml` workflow, which builds a preview and posts the URL as a PR comment. Requires `NETLIFY_AUTH_TOKEN` and `NETLIFY_SITE_ID` secrets.

## GitHub Secrets

| Secret | Purpose |
|--------|---------|
| `NETLIFY_AUTH_TOKEN` | Netlify authentication for PR previews |
| `NETLIFY_SITE_ID` | Netlify site ID for PR previews |

## Pages

Folders with multiple .md files inside will have multiple chapters. If the .md file is on the /pages parent folder, it will be single chapter.

## Markdown Formatting

# Sample Figure

{numref}`fig-sample` shows a sample bar chart generated with Matplotlib.

```{figure} ../images/sample_figure.png
:name: fig-sample
:alt: A sample bar chart

A sample bar chart showing values for five categories.
```

# Dropdown Example:

:::{dropdown} 2025
:open:

- Item 1
- Item 2
- Item 3

:::

:::{dropdown} 2024

- Item 1
- Item 2
- Item 3

:::

# Code Example:

```{code-cell} ipython3
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 2 * np.pi, 100)
y = np.sin(x)

fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_xlabel("x")
ax.set_ylabel("sin(x)")
ax.set_title("A Simple Plot")
plt.show()
```

# Sample Table

The table below shows an overview of the key tools used in this book.

```{list-table} Overview of key tools
:header-rows: 1
:name: tab-tools

* - Tool
  - Description
  - Version
* - Python
  - Programming language
  - 3.12
* - NumPy
  - Numerical computing library
  - 1.26
* - Matplotlib
  - Plotting and visualization
  - 3.8
* - MyST
  - Markdown authoring framework
  - 1.8
```

# Video Link Sample

:::{iframe} https://www.youtube.com/embed/KiceHVININs
:width: 100%
Video tutorial: Build a Professional CV Website with Auto PDF Generation
:::

## Add Blog Posts

The template includes a built-in blog. To add a new post:

1. Create a new Markdown file in the `blog/` directory (e.g., `blog/my-first-post.md`).
2. Add YAML frontmatter with `title`, `date`, `description`, and other metadata.
3. Write your content in Markdown.
4. Open `pages/blog.md` (or `blog.md`, depending on the template version) and add a new `:::{card}` entry inside the grid:

```markdown
:::{card} My First Blog Post
:link: ./blog/my-first-post
April 10, 2026 – A short description of the post.
:::
```

The grid layout (`1 1 2 2`) means one column on small screens and two columns on larger screens, keeping the layout responsive.

The template also generates RSS and Atom feeds automatically, so readers can subscribe to your blog. The feed links appear on the blog index page.

## Deploy and Verify

Once you are happy with your changes, commit and push:

```bash
git add .
git commit -m "Update website content"
git push
```

GitHub Actions will:

1. Build the HTML site with `myst build –html`.
2. Download fonts for the CV.
3. Run `generate_cv.py` to produce the Typst source.
4. Compile the PDF with Typst.
5. Deploy everything to GitHub Pages.

After a minute or two, visit your site and click the CV link. The PDF is served at a stable URL (`https://username.github.io/repo-name/cv.pdf`) that you can share with anyone. It includes bookmarks and a clickable table of contents for easy navigation, especially useful as your CV grows longer.

## Using Pull Requests

For larger changes, consider creating a feature branch and opening a pull request instead of pushing directly to `main`. The template includes a pre-commit configuration that catches typos, trailing whitespace, and formatting issues. This workflow also triggers a Netlify preview deployment so you can review your changes before merging.

## Responsive Layout and Theming

The site uses the MyST book theme, which supports both light and dark modes. The layout is responsive – grid components like `::::{grid} 2 2 4 4` show two columns on small screens and four on large screens. You can adjust these numbers on any grid to fit your content.

For further visual customization, the template includes a `custom.css` file where you can override theme defaults without modifying the MyST source.

## License

[MIT](LICENSE)
