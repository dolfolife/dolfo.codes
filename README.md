# dolfo.codes

Personal blog built with [Hugo](https://gohugo.io/) using the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme.

## Prerequisites

- [Hugo](https://gohugo.io/installation/) v0.112.4 or later (Extended version recommended)
  - Tested with Hugo v0.151.0+extended
- Git

## Getting Started

### Clone the Repository

This repository uses git submodules for the theme, so make sure to clone with the `--recursive` flag:

```bash
git clone --recursive https://github.com/dolfolife/dolfo.codes.git
cd dolfo.codes
```

If you've already cloned the repository without the `--recursive` flag, initialize the submodules:

```bash
git submodule update --init --recursive
```

**Important:** Ensure the theme is on the `master` branch for best compatibility:

```bash
cd themes/papermod
git checkout master
cd ../..
```

### Running Locally

To start the development server:

```bash
hugo serve
```

The site will be available at `http://localhost:1313`

Hugo will watch for changes and automatically reload the browser.

### Building for Production

To build the static site for production:

```bash
hugo
```

The generated files will be in the `public/` directory.

## Troubleshooting

### Subresource Integrity (SRI) Error

If you encounter an error like:
```
Failed to find a valid digest in the 'integrity' attribute for resource
```

This typically happens when cached files have mismatched integrity hashes. To fix:

```bash
# Remove generated files and cached assets
rm -rf public/
rm -rf resources/_gen/

# Ensure the theme submodule is properly initialized
git submodule update --init --recursive

# Make sure the theme is on master branch (compatible with Hugo 0.151+)
cd themes/papermod
git checkout master
cd ../..

# Start the server again
hugo serve
```

### Theme Not Found Error

If Hugo can't find the theme, make sure the submodule is initialized:

```bash
git submodule update --init --recursive
```

### Layout Warnings or Template Errors

If you see warnings about missing layouts or template errors, ensure the theme is on the `master` branch:

```bash
cd themes/papermod
git checkout master
cd ../..
hugo serve
```

The theme's tagged versions (v7.0, v8.0) may have compatibility issues with newer Hugo versions. The `master` branch is the most stable.

## Project Structure

```
.
├── content/           # Markdown content files
│   ├── posts/        # Blog posts
│   └── search.md     # Search page
├── static/           # Static assets (images, etc.)
├── themes/           # Hugo themes (git submodule)
│   └── papermod/     # PaperMod theme
├── public/           # Generated site (git ignored)
├── resources/        # Hugo cache (git ignored)
├── hugo.yaml         # Hugo configuration
└── CNAME             # Custom domain configuration
```

## Configuration

The site is configured through `hugo.yaml`. Key settings include:

- **Base URL**: `https://dolfo.codes/`
- **Theme**: PaperMod
- **Features**: Search, RSS, code highlighting, reading time, TOC

## Writing Posts

Create a new post:

```bash
hugo new posts/my-new-post.md
```

Posts are stored in `content/posts/` and use markdown format with YAML frontmatter.

## Deployment

This site is configured to deploy to GitHub Pages (indicated by the CNAME file). The `public/` directory contains the built site.

## License

Content is © Rodolfo Sanchez. Code is available under the MIT license.

