# GitHub Actions Setup Guide

This repository includes automated workflows for PR validation and preview deployments.

## Workflows Overview

### 1. PR Validation (`pr-validation.yml`)
✅ **Active** - No setup required

This workflow automatically:
- Builds the Zola site on every PR
- Validates the build output
- Checks for broken internal links
- Posts build statistics as PR comments
- Uploads build artifacts for manual review

### 2. PR Preview Deployments

Two options are provided. Choose one based on your preference:

#### Option A: Cloudflare Pages (`pr-preview.yml`)
**Current default** - Requires setup

**Setup Steps:**
1. Create a Cloudflare account at https://cloudflare.com
2. Go to Workers & Pages → Create application → Pages → Connect to Git
3. Get your Account ID from the URL or dashboard
4. Create an API token at https://dash.cloudflare.com/profile/api-tokens
   - Use the "Edit Cloudflare Workers" template
   - Add "Cloudflare Pages" permissions
5. Add secrets to your GitHub repository (Settings → Secrets → Actions):
   - `CLOUDFLARE_API_TOKEN`: Your API token
   - `CLOUDFLARE_ACCOUNT_ID`: Your account ID
6. Update the project name in `pr-preview.yml` (line 32):
   ```yaml
   command: pages deploy public --project-name=YOUR-PROJECT-NAME --branch=pr-${{ github.event.pull_request.number }}
   ```

**Preview URL format:** `https://pr-{number}.your-project.pages.dev`

#### Option B: Netlify (`pr-preview-netlify.yml.example`)
Alternative option - Requires setup

**Setup Steps:**
1. Rename `pr-preview-netlify.yml.example` to `pr-preview-netlify.yml`
2. Delete or rename `pr-preview.yml` to disable it
3. Create a Netlify account at https://netlify.com
4. Create a new site (you can use drag-and-drop with a dummy folder)
5. Get your Site ID from Site settings → General → Site details
6. Create a Personal Access Token at User settings → Applications → Personal access tokens
7. Add secrets to your GitHub repository:
   - `NETLIFY_AUTH_TOKEN`: Your personal access token
   - `NETLIFY_SITE_ID`: Your site ID

**Preview URL format:** `https://pr-{number}--your-site.netlify.app`

## Disabling Preview Deployments

If you don't want preview deployments:
1. Delete both `pr-preview.yml` and `pr-preview-netlify.yml.example`
2. Keep only `pr-validation.yml` for build validation

## Testing the Workflows

To test the workflows:
1. Create a test branch
2. Make a small change (e.g., edit README.md)
3. Open a pull request
4. Check the Actions tab to see workflows running
5. Look for bot comments on the PR with build status and preview URLs

## Troubleshooting

### PR Validation fails
- Check the Actions tab for detailed error messages
- Ensure all submodules are properly initialized
- Verify that the Zola build works locally

### Preview deployment fails
- Verify all secrets are correctly set
- Check that secret names match exactly
- Ensure your API tokens have the correct permissions
- Review the Actions logs for specific error messages

### No bot comments on PR
- Ensure the workflow has `pull-requests: write` permission
- Check that the workflow completed successfully
- Verify GitHub Actions has permission to comment (Settings → Actions → General)

## Security Notes

- Never commit API tokens or secrets to the repository
- Use GitHub Secrets for all sensitive data
- Regularly rotate your API tokens
- Review workflow permissions regularly

## Support

For issues with:
- **Workflows**: Check the Actions tab and logs
- **Cloudflare Pages**: https://developers.cloudflare.com/pages/
- **Netlify**: https://docs.netlify.com/
- **GitHub Actions**: https://docs.github.com/en/actions
