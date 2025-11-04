# Alternative Workflow with PAT Token Support

If you want the workflow to automatically convert PRs to draft status when requirements aren't met, you'll need to use a Personal Access Token (PAT) with elevated permissions.

## Setup Instructions

### 1. Create a Personal Access Token

1. Go to GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate a new token with these permissions:
   - `repo` (Full control of private repositories)
   - `public_repo` (Access to public repositories)

### 2. Add Repository Secret

1. In your repository, go to Settings → Secrets and variables → Actions
2. Create a new repository secret named `GH_ADMIN_TOKEN`
3. Paste your PAT token as the value

### 3. Update Workflow

Replace the warning comments approach with these steps in your workflow:

```yaml
      - name: Convert to draft if requirements not met
        if: steps.check-requirements.outputs.all_required_complete == 'false' && github.event.pull_request.draft == false
        run: |
          # Convert PR to draft
          gh pr ready --undo ${{ github.event.pull_request.number }}
          
          # Add comment explaining why
          gh pr comment ${{ github.event.pull_request.number }} --body "🚧 **This PR has been converted to draft status**

          The first three checkboxes in the PR template must be completed before this PR can be reviewed:
          
          - [ ] You've provided a link to documentation where the project has approved the maintainer changes.
          - [ ] The maintainer(s) also created or updated their LFX Individual Dashboard profile.
          - [ ] You've sent an email with the email address(es) to cncf-maintainer-changes@cncf.io for invitations to Service Desk and mailing lists.
          
          Please complete these requirements and mark the checkboxes as complete, then mark this PR as ready for review."
        env:
          GH_TOKEN: ${{ secrets.GH_ADMIN_TOKEN }}

      - name: Mark as ready for review if requirements met
        if: steps.check-requirements.outputs.all_required_complete == 'true' && github.event.pull_request.draft == true
        run: |
          gh pr ready ${{ github.event.pull_request.number }}
        env:
          GH_TOKEN: ${{ secrets.GH_ADMIN_TOKEN }}
```

## Security Considerations

- PAT tokens have elevated permissions - store them securely
- Consider using fine-grained personal access tokens for better security
- Review token permissions regularly
- Consider if the warning-comment approach is sufficient for your workflow

## Current Workflow

The current workflow uses a permissions-friendly approach that:
- ✅ Posts warning comments when requirements aren't met
- ✅ Posts approval comments when requirements are complete  
- ✅ Works with default `GITHUB_TOKEN` permissions
- ✅ Doesn't require additional secrets or setup
- ❌ Doesn't automatically convert PRs to draft status

Choose the approach that best fits your repository's security requirements and workflow needs.