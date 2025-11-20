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

To support forked repositories, this workflow requires a fine-grained Personal Access Token with repository-specific permissions:

1. **Create a fine-grained PAT**:
   - Go to GitHub Settings → Developer settings → Personal access tokens → Fine-grained tokens
   - Click "Generate new token"
   - Set **Resource owner** to your username or organization
   - Under **Repository access**, select "Selected repositories" and choose this repository
   - Set the **Expiration** (recommend 1 year maximum for security)
   - Under **Repository permissions**, grant:
     - Contents: Read
     - Issues: Write
     - Pull requests: Write
     - Metadata: Read

2. **Add the PAT as a repository secret**:
   - Go to your repository Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Name: `MAINTAINER_VALIDATION_TOKEN`
   - Value: Your personal access token

3. **Why fine-grained tokens are preferred**:
   - **Security**: Scoped to only this repository, not all your repositories
   - **Principle of least privilege**: Only the exact permissions needed
   - **Fork support**: Can comment on pull requests from forked repositories
   - **Auditing**: Clear visibility into which repository the token accesses
   - **Expiration**: Built-in token rotation for better security hygiene

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

1. **"Context access might be invalid: MAINTAINER_VALIDATION_TOKEN" warning**:
   - This is a linter warning, not an error
   - The workflow will function correctly once the MAINTAINER_VALIDATION_TOKEN secret is configured

2. **Comments not appearing on PRs from forks**:
   - Verify the MAINTAINER_VALIDATION_TOKEN secret is configured correctly
   - Ensure the fine-grained token has the required repository permissions
   - Check that the token hasn't expired

3. **"Resource not accessible by personal access token" error**:
   - The fine-grained token may not have sufficient permissions
   - Verify the token is scoped to the correct repository
   - Ensure Issues: Write and Pull requests: Write permissions are granted

4. **CSV validation failures**:
   - Check CSV syntax with proper escaping
   - Ensure project inheritance follows the expected format

### Testing

Test the workflows by:

1. Creating a PR with maintainer changes
2. Verifying all checklist items are completed
3. Confirming automated comments appear with change summaries
