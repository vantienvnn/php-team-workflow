Git process workflow
=====================

Please following our GIT convention requirement:

- Fork project repository to your GitHub account and please make sure you don't working on project repository.
- Create one branch from test branch for each your task on JIRA
- When you do finished your task:
  - Rebase your branch with test branch in Project Repository
  - Make sure one commit for one Pull Request, else plesae combine it
  - Create a Pull Request on Github in Your Repostiory to Project Repository
  - Make sure you will Pull Request to test branch in Project Repository
  - The Pull Request name should be like this format: Task {task-name}
  - The Pull Request description should have JIRA task URL
- When you do created your Pull Request:
  - If have conflict message form Github you are forgot rebase test branch from Project Repository
  - You can pick other task on waiting Simble CI checking your Pull Request
  - Please send a message to our team group chat in Slack when the Simble CI status is green
  - If Simble CI status have red, you can check error message in link of Simble CI status
  - When you push new code to your branch, the Pull Request will auto update and the Simble CI will re-build again.
    So please don't push code again if you are not have checked you task

How to Fork project repository?
=====================
For example: 
  - Project repository: https://github.com/project-username/childspass
  - Your repository: https://github.com/your-username/childspass
  
Forking a repository is a simple two-step process. We've created a repository for you to practice with!
- On GitHub, navigate to the octocat/Spoon-Knife repository.
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



