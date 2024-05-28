#### [Back](./README.md)

# List of Events that trigger Workflow
<a href="https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows" target="_blank">here</a>

1. **branch_protection_rule**
2. **check_run**
3. **check_suite**
4. **create**
5. **delete**
6. **deployment**
7. **deployment_status**
8. **discussion**
9. **discussion_comment**
10. **fork**
11. **gollum**
12. **issue_comment**
13. **issues**
14. **label**
15. **merge_group**
16. **milestone**
17. **page_build**
18. **project**
19. **project_card**
20. **project_column**
21. **public**
22. **pull_request**
23. **pull_request_comment (use issue_comment)**
24. **pull_request_review**
25. **pull_request_review_comment**
26. **pull_request_target**
27. **push** 

    Runs your workflow when you push a commit or tag, or when you create a repository from a template.
    
    **Example:-**
    ```yaml
    on:
        push
    ```
    
    **Example Push to Specific Branch:-**
    ```yaml
    on:
        push:
            branches:
                - 'main'
                - 'releases/**'
    ```

    **Example with filter:-**
    the following workflow will only run when a push that includes a change to a JavaScript (.js) file is made to a branch whose name starts with releases/:
    ```yaml
    on:
        push:
            branches:
                - 'releases/**'
            paths:
                - '**.js'    
    ```
    
    **Example Push to Specific Tag:-**
    ```yaml
    on:
        push:
            tags:
                - v1.**
    ```

    **Example Push to Specific File:-**
    ```yaml
    on:
        push:
            paths:
                - '**.js'
    ```


28. **registry_package**
29. **rebase**
30. **repository_dispatch**
31. **schedule**
    * The schedule event can be delayed during periods of high loads of GitHub Actions workflow runs. High load times include the start of every hour. If the load is sufficiently high enough, some queued jobs may be dropped. To decrease the chance of delay, schedule your workflow to run at a different time of the hour.
    * This event will only trigger a workflow run if the workflow file is on the default branch.
    * Scheduled workflows will only run on the default branch.
    * In a public repository, scheduled workflows are automatically disabled when no repository activity has occurred in 60 days.
    * When the last user to commit to the cron schedule of a workflow is removed from the organization, the scheduled workflow will be disabled. If a user with write permissions to the repository makes a commit that changes the cron schedule, the scheduled workflow will be reactivated. Note that, in this situation, the workflow is not reactivated by any change to the workflow file; you must alter the cron value and commit this change.
    * Notifications for scheduled workflows are sent to the user who last modified the cron syntax in the workflow file.


    **Example:-**
    ```yaml
    on:
        schedule:
            - cron: "15 4,5 * * *"   # <=== Change this value
    ```

    **Example Multiple Schedule Events:-**
    ```yaml
    on:
        schedule:
            - cron: '30 5 * * 1,3'
            - cron: '30 5 * * 2,4'
    jobs:
        test_schedule:
            runs-on: ubuntu-latest
            steps:
                - name: Not on Monday or Wednesday
                  if: github.event.schedule != '30 5 * * 1,3'
                  run: echo "This step will be skipped on Monday and Wednesday"
                - name: Every time
                  run: echo "This step will always run"
    ```
    **GitHub Actions does not support the non-standard syntax @yearly, @monthly, @weekly, @daily, @hourly, and @reboot**

32. **status**
33. **watch**
34. **workflow_call**
35. **workflow_dispatch**
36. **workflow_run**