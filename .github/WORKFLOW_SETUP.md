# Maintainer PR Validation Setup

This repository includes GitHub Actions workflows to validate pull requests that modify the `project-maintainers.csv` file.

## Workflows

### 1. CSV Syntax Validation (`validate-csv.yml`)

- Validates CSV syntax using the [csv-lint action](https://github.com/krook/csv-lint)
- Runs on all PRs that modify `project-maintainers.csv`

### 2. Maintainer PR Validation (`maintainer-pr-validation.yml`)

- Validates that required checklist items are completed in PR template
- Automatically converts PRs to draft status if requirements aren't met
- Analyzes changes and posts formatted summaries as PR comments when ready
- Generates change summaries in both CSV and Markdown table formats

## No Configuration Required

This workflow uses only the built-in `GITHUB_TOKEN` and doesn't require any additional secrets or external services.

## How it Works

### PR Checklist Validation

The workflow checks for these completed checkboxes in the PR description:

- [x] You've provided a link to documentation where the project has approved the maintainer changes.
- [x] The maintainer(s) also created or updated their LFX Individual Dashboard profile.
- [x] You've sent an email with the email address(es) to <cncf-maintainer-changes@cncf.io> for invitations to Service Desk and mailing lists.

### Change Detection

The workflow analyzes the CSV diff to categorize changes as:

- **Add**: New maintainer entries
- **Update**: Modified existing entries
- **Remove**: Deleted entries

### GitHub Comment Summary

When a PR is ready for review with completed checklist items, the workflow:

1. Analyzes CSV changes to detect Add/Update/Remove operations
2. Generates a formatted Markdown table with change details
3. Posts a comment on the PR with the summary table
4. Uploads CSV and Markdown artifacts for record keeping

The comment includes a table like this:

| Project | Maintainer Name | Company | Email | GitHub Handle | Change |
|---------|-----------------|---------|-------|---------------|--------|
| Kubernetes | John Doe | Example Corp | _To be filled manually_ | johndoe | ✅ Add |

## Manual Steps

After the workflow posts the summary comment:

1. Review the changes table in the PR comment
2. Fill in email addresses for each maintainer manually
3. Process the changes according to your organization's procedures
4. Update any necessary systems or send additional notifications

## Troubleshooting

- **Checkboxes not detected**: Ensure checkboxes use `[x]` format with exact text matching
- **Changes not detected**: Verify the CSV structure matches expected format with proper columns
- **Table formatting issues**: Check for special characters that might break Markdown table formatting
