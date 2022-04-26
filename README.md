# Github Actions Repo
This repo is designed to house github actions that we use in our workflows.  It has been moved from public to private.

# Versioning
In order to make it easier to add, update, and use these actions, we are using branches for versioning.  An action is ferred to via it's full path and version, eg `Nexben/github-actions/.github/workflows/feature-branch-deploy.yml@v4`.  This would reference the action 'feature-branch-deploy' version 4 in the repo 'Nexben/github-actions'

# Current Actions

## Feature-Branch-Deploy
This action triggers the the matching deployment AWS CodePipeline for this repo.  See example usage below

```yaml
aws-deploy:
    needs: [vars, create-release]
    uses: Nexben/github-actions/.github/workflows/feature-branch-deploy.yml@v4
    with:
      repository_name: ${{ github.event.repository.full_name }}
      branch_name: ${{ needs.vars.outputs.app_branch }}
      service_name: ${{ needs.vars.outputs.service_name }}
    secrets:
      slack_webhook: '${{ secrets.SLACK_NOTIFY_WEBHOOK }}'
      aws_access_key_id: '${{ secrets.AWS_TOOLS_DEPLOYMENT_ACCESS_KEY_ID }}'
      aws_secret_access_key: '${{ secrets.AWS_TOOLS_DEPLOYMENT_SECRET_ACCESS_KEY }}'
      aws_region: '${{ secrets.AWS_TOOLS_REGION }}'
      pipeline_table_name: '${{ secrets.AWS_TOOLS_PIPELINE_EXECUTIONS_TABLE_NAME }}'
```

# Here be dragons
The actions in this repo can be used by a lot of repos.  Please contact the Platform Engineering team before making changes to it.  Thanks!
