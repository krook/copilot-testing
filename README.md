# copilot-testing

This repository contains automated workflows for validating maintainer changes in CSV files.

## Features

- **Automated CSV Validation**: Syntax and formatting checks on every pull request
- **Maintainer Change Analysis**: Intelligent analysis of maintainer updates with project inheritance
- **Fork Support**: Works with pull requests from forked repositories
- **Interactive Guidance**: Automated comments with detailed summaries and next steps

## Quick Start

1. **For Contributors**: When submitting maintainer changes, ensure all checklist items in the PR template are completed
2. **For Repository Maintainers**: Configure the `MAINTAINER_VALIDATION_TOKEN` secret for full functionality

## Setup Requirements

### Token Configuration (Repository Maintainers)

To enable full workflow functionality including fork support:

1. Create a fine-grained Personal Access Token:
   - Go to GitHub Settings → Developer settings → Personal access tokens → Fine-grained tokens
   - Scope to this repository with permissions: Contents (Read), Issues (Write), Pull requests (Write), Metadata (Read)

2. Add as repository secret:
   - Repository Settings → Secrets and variables → Actions
   - Name: `MAINTAINER_VALIDATION_TOKEN`
   - Value: Your token

## Files

- `project-maintainers.csv` - Main maintainer data file
- `.github/workflows/` - Automated validation workflows
- `.github/pull_request_template.md` - PR checklist template

For detailed workflow documentation, see [.github/workflows/README.md](.github/workflows/README.md).
