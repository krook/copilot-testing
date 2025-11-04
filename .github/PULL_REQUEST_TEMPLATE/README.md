# PR Templates

This repository uses multiple PR templates to provide targeted guidance for different types of contributions.

## Available Templates

### 🔗 How to Use Templates

When creating a new PR, you can select a specific template by adding `?template=<template_name>` to the PR creation URL:

1. **Maintainer Updates**: `?template=maintainer_update.md`
   - For changes to `project-maintainers.csv`
   - Includes required checklist and documentation requirements
   - Automatically validated by GitHub Actions workflow

2. **General Changes**: `?template=general.md`  
   - For code changes, documentation, workflows, etc.
   - Standard PR template with testing checklist

### 🚀 Quick Links

- [Create Maintainer Update PR](../../compare?template=maintainer_update.md)
- [Create General Change PR](../../compare?template=general.md)

### 📋 Template Structure

```
.github/
├── pull_request_template.md           # Default template with instructions
└── PULL_REQUEST_TEMPLATE/
    ├── maintainer_update.md           # For CSV maintainer changes
    └── general.md                     # For other changes
```

## Workflow Integration

The `maintainer-pr-validation.yml` workflow automatically:
- Detects when `project-maintainers.csv` is modified
- Validates the first 3 checkboxes are completed
- Generates change summaries with Markdown tables
- Posts comments with required next steps

## Need Help?

- Review [WORKFLOW_SETUP.md](../WORKFLOW_SETUP.md) for detailed workflow information
- Contact repository maintainers for guidance on template selection