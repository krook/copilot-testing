# GitHub Actions Workflows

This directory contains automated workflows for validating maintainer changes in the CSV file.

## Workflows

### validate-csv.yml

- Validates CSV syntax and formatting
- Runs on every pull request
- Uses the `krook/csv-lint` action

### validate-maintainers.yml

- Validates PR checklist requirements
- Analyzes maintainer changes with project inheritance
- Posts detailed summaries and guidance
- Supports forked repositories with proper token configuration

## Setup Requirements

### Personal Access Token (PAT) Configuration

To support forked repositories, this workflow requires a Personal Access Token with appropriate permissions:

1. **Create a PAT**:
   - Go to GitHub Settings → Developer settings → Personal access tokens → Fine-grained tokens
   - Create a new token with these permissions for this repository:
     - Contents: Read
     - Issues: Write
     - Pull requests: Write
     - Metadata: Read

2. **Add the PAT as a repository secret**:
   - Go to your repository Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `PAT_TOKEN`
   - Value: Your personal access token

3. **Why this is needed**:
   - The default `GITHUB_TOKEN` has limited permissions on forked repositories
   - It cannot comment on pull requests from forks for security reasons
   - A PAT with proper permissions enables cross-fork communication

### Workflow Permissions

The workflows also require these repository permissions:

- Actions: Read
- Contents: Read
- Issues: Write
- Pull requests: Write

## Pull Request Template

The `pull_request_template.md` provides a checklist for maintainer changes:

- ✅ I have updated the maintainer information accurately
- ✅ I have verified the project inheritance is correct
- ✅ I understand that maintainer changes require careful review

## Troubleshooting

### Common Issues

1. **"Context access might be invalid: PAT_TOKEN" warning**:
   - This is a linter warning, not an error
   - The workflow will function correctly once the PAT_TOKEN secret is configured

2. **Comments not appearing on PRs from forks**:
   - Verify the PAT_TOKEN secret is configured correctly
   - Ensure the PAT has the required permissions listed above

3. **CSV validation failures**:
   - Check CSV syntax with proper escaping
   - Ensure project inheritance follows the expected format

### Testing

Test the workflows by:

1. Creating a PR with maintainer changes
2. Verifying all checklist items are completed
3. Confirming automated comments appear with change summaries