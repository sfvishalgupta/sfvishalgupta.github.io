#### [Back](../Componants.md)

# Component ON

To automatically trigger a workflow, use on to define which events can cause the workflow to run.

You can define single or multiple events that can trigger a workflow, or set a time schedule. You can also restrict the execution of a workflow to only occur for specific files, tags, or branch changes.

**Using Single Event**
```bash
on: push
```

**Using Multiple Event**
```yaml
on: [push, fork]
```

**Using Activity Type**
```yaml
on:
  issues:
    types:
      - opened
      - labeled
```

**Using Filters**
```yaml
on:
  push:
    branches:
      - main
      - 'releases/**'
```

**Using activity types and filters with multiple events**
```yaml
on:
  label:
    types:
      - created
  push:
    branches:
      - main
  page_build:
```
