#### [Back](../Componants.md)

# Component Permissions

You can use permissions to modify the default permissions granted to the GITHUB_TOKEN, adding or removing access as required, so that you only allow the minimum required access.

You can use permissions either as a top-level key, to apply to all jobs in the workflow, or within specific jobs. When you add the permissions key within a specific job, all actions and run commands within that job that use the GITHUB_TOKEN gain the access rights you specify. 

**Scope**
1. **actions:** 
Work with GitHub Actions. For example, actions: write permits an action to cancel a workflow run.

2. **attestations:** 
Work with artifact attestations. For example, attestations: write permits an action to generate an artifact attestation for a build. 

3. **checks** 
Work with check runs and check suites. For example, checks: write permits an action to create a check run. 

4. **contents:**
Work with the contents of the repository. For example, contents: read permits an action to list the commits, and contents: write allows the action to create a release. 

5. **deployments:**
Work with deployments. For example, deployments: write permits an action to create a new deployment.

6. **discussions**
Work with GitHub Discussions. For example, discussions: write permits an action to close or delete a discussion.

7. **id-token:**
Fetch an OpenID Connect (OIDC) token. This requires id-token: write.

8. **issues:**
Work with issues. For example, issues: write permits an action to add a comment to an issue.

9. **packages:**
Work with GitHub Packages. For example, packages: write permits an action to upload and publish packages on GitHub Packages. 

10. **pages:**
Work with GitHub Pages. For example, pages: write permits an action to request a GitHub Pages build. 

11. **pull-requests:**
Work with pull requests. For example, pull-requests: write permits an action to add a label to a pull request. 

12. **repository-projects:**
Work with GitHub projects (classic). For example, repository-projects: write permits an action to add a column to a project (classic).

13. **security-events:**
Work with GitHub code scanning and Dependabot alerts. For example, security-events: read permits an action to list the Dependabot alerts for the repository, and security-events: write allows an action to update the status of a code scanning alert.

14. **statuses:**
Work with commit statuses. For example, statuses:read permits an action to list the commit statuses for a given reference.

```yaml
permissions:
  actions: read|write|none 
  checks: read|write|none
  contents: read|write|none
  deployments: read|write|none
  id-token: read|write|none
  issues: read|write|none
  discussions: read|write|none
  packages: read|write|none
  pages: read|write|none
  pull-requests: read|write|none
  repository-projects: read|write|none
  security-events: read|write|none
  statuses: read|write|none
```

* If you specify the access for any of these scopes, all of those that are not specified are set to none.

* You can use the following syntax to define one of read-all or write-all access for all of the available scopes:
```yaml
permissions: read-all
```

```yaml
permissions: write-all
```

* You can use the following syntax to disable permissions for all of the available scopes:
```yaml
permissions: {}
```