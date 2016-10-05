Git process workflow
=====================

Please following our GIT convention requirement:

- Fork project repository to your GitHub account
- Make sure you do not push, merge to project repository
- Create one branch from test branch for each your tasks on JIRA
- When you do finished your task:
  - Rebase your branch with test branch in Project Repository
  - Make sure one commit for one Pull Request ( PR )
  - Create a PR on Github in your repostiory to test branch of project repository
  - Name of PR should be like this format: Task {task-name}
  - Description of PR should have JIRA task URL
- When you do created your PR:
  - If have conflict message form Github you are forgot rebase
  - You can pick other task on waiting Simble CI checking your PR
  - Please send a message to our team group chat in Slack when the Simble CI status is succeed
  - If Simble CI status is failed
    - Check error message in link of Simble CI status
    - Just re-update (push) your branch when you have test you code are fixed all errors

How to Fork project repository?
=====================
For example: 
  - Project repository: https://github.com/project-username/childspass
  - Your repository: https://github.com/your-username/childspass
  
Forking a repository is a simple two-step process. We've created a repository for you to practice with!
- On GitHub, navigate to the project-username/childspass repository.
- Fork buttonIn the top-right corner of the page, click Fork.

![Settings Window](https://raw.github.com/vantienvnn/php-team-workflow/master/images/fork.PNG)

Example git comamnd:

```php
// clone to your local
git clone https://github.com/your-username/childspass.git
// add upstream to project repository
git remote add upstream https://github.com/project-username/childspass.git
// update data from your repository and project repository
git fetch --all
```

For more information, you can read [here](https://help.github.com/articles/fork-a-repo/)



