#### [Back](./README.md)

# Components Of Workflow

### name
The name of the workflow. GitHub displays the names of your workflows under your repository's "Actions" tab. If you omit name, GitHub displays the workflow file path relative to the root of the repository.

### run-name
The name for workflow runs generated from the workflow. GitHub displays the workflow run name in the list of workflow runs on your repository's "Actions" tab. If run-name is omitted or is only whitespace, then the run name is set to event-specific information for the workflow run. For example, for a workflow triggered by a push or pull_request event, it is set as the commit message or the title of the pull request.

**Example of run-name**
```yaml
run-name: Deploy to ${{ inputs.deploy_target }} by @${{ github.actor }}
```

### [on](./Componants/on.md)
### [permissions](./Componants/permissions.md)
### default
### concurrency
### jobs


