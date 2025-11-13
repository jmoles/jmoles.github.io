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

This site is deployed to GitHub Pages. The build process should be configured in a GitHub Actions workflow to build the Zola site and deploy it.
