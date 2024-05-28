#### [Back](./README.md)

# Actions

The actions used in workflow can be defined in

1. Same repo of workflow.
2. Public Repo
3. Published docker container image on Docker hub.

## Adding action from same repo.

```bash
|-- hello-world (repository)
|   |__ .github
|       └── workflows
|           └── my-first-workflow.yml
|       └── actions
|           |__ hello-world-action
|               └── action.yml
```

Example Workflow File

```yaml
jobs:
  my_first_job:
    runs-on: ubuntu-latest
    steps:
      # This step checks out a copy of your repository.
      - name: My first step - check out repository
        uses: actions/checkout@v4
      # This step references the directory that contains the action.
      - name: Use local hello-world-action
        uses: ./.github/actions/hello-world-action
```

## Adding action from different repo

If an action is defined in a different repository than your workflow file, you can reference the action with the **{owner}/{repo}@{ref}** syntax in your workflow file.

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: actions/setup-node@v4
```

## Referencing a container on Docker Hub
If an action is defined in a published Docker container image on Docker Hub, you must reference the action with the docker://{image}:{tag} syntax in your workflow file.

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
```

## Release Management for Custom Action
1.  Using Tags
```yaml
steps:
  - uses: actions/javascript-action@v1.0.1
```

2.  Using SHA
```yaml
steps:
  - uses: actions/javascript-action@a824008085750b8e136effc585c3cd6082bd575f
```

3.  Using Branches
```yaml
steps:
  - uses: actions/javascript-action@main
```

### Using Input and Output with Actions
An action often accepts or requires inputs and generates outputs that you can use. 
```yaml
name: "Example"
description: "Receives file and generates output"
inputs:
  file-path: # id of input
    description: "Path to test script"
    required: true
    default: "test-file.js"
outputs:
  results-file: # id of output
    description: "Path to results file"

```