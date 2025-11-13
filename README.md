# jmoles.github.io

Personal website built with [Zola](https://www.getzola.org/) using the [anemone](https://github.com/Speyll/anemone) theme.

## Building the site

1. Install Zola: https://www.getzola.org/documentation/getting-started/installation/
2. Initialize the theme submodule (if not already done):
   ```bash
   git submodule update --init --recursive
   ```
3. Build the site:
   ```bash
   zola build
   ```
4. Or serve it locally:
   ```bash
   zola serve
   ```

The built site will be in the `public/` directory.

## Deployment

This site is automatically deployed to GitHub Pages via GitHub Actions when changes are pushed to the `main` branch.

### GitHub Actions Workflows

This repository includes several automated workflows:

- **Deploy to GitHub Pages** (`.github/workflows/deploy.yml`) - Automatically deploys the site when changes are pushed to main
- **PR Validation** (`.github/workflows/pr-validation.yml`) - Validates builds and checks for issues on pull requests
- **PR Preview Deployment** (`.github/workflows/pr-preview.yml`) - Creates preview deployments for pull requests (requires setup)

See [.github/SETUP.md](.github/SETUP.md) for detailed setup instructions for PR preview deployments.
