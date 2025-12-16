# Personal Portfolio

This is the source code for my personal portfolio website, built with [Zola](https://www.getzola.org/) - a fast static site generator written in Rust.

## Overview

A clean, modern portfolio showcasing my research, projects, publications, and blog posts on machine learning and AI.

## Built With

- **Zola** - Static site generator
- **HTML/CSS** - Markup and styling
- **Markdown** - Content

## Getting Started

### Prerequisites

- [Zola](https://www.getzola.org/documentation/getting-started/installation/) installed

### Running Locally

```bash
# Clone the repository
git clone <repository-url>
cd personalpage

# Serve the site locally
zola serve
```

The site will be available at `http://127.0.0.1:1111`

### Building for Production

```bash
zola build
```

This generates a `public` directory with the static site ready for deployment.

## Structure

- `content/` - Blog posts and content
- `templates/` - HTML templates
- `static/` - Static assets (CSS, images, etc.)
- `config.toml` - Site configuration

## License

© 2025 Akash Kamalesh. All rights reserved.
