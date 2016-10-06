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

How to create new branch for each task?
=====================
If your task on JIRA is named are SIM 201, so you should create a branch like as:
```php
git checkout -b sim-201 origin/test
```

How about have one commit for PR?
=====================
For the first commit:
```php
git add .
git commit -m "Implement task sim-201"
git push origin <branch-name>
```
From second commit:
```php
git add .
git commit --amend
git push origin <branch-name> -f
```
One popup will show when you commit with --amend
![Settings Window](https://raw.github.com/vantienvnn/php-team-workflow/master/images/commit_amend.PNG)
- In this screen you can change the commit message (green/yellow area)
- To save this please follow as bellow
  - Linux: Ctrl+X -> Yes -> Enter
  - Window/MAC: Esc -> Shift + : + wq + Enter

If you forgot --amend from seconds commit, please don't worry, we can combine it as bellow
```php
git log --oneline
```
One popup will show as bellow:
![Settings Window](https://raw.github.com/vantienvnn/php-team-workflow/master/images/commit_log.PNG)
- Enter q for exit this popup
So If your first commit is hightlight line:
```php
git reset e0d11dd
git add .
git commit --amend
git push origin <branch-name> -f
```

How to rebase your branch with project repository branch?
=====================
Please make sure your are added upstream as above document
```php
git fetch --all
git rebase upstream/test
```

How to update other member PR to your local?
=====================
Fetch to your local and create new branch for test:
```php
// git fetch upstream  pull/<pull request id>/head:<new branch name in your local>
git fetch upstream pull/12/head:test-kapo-task-sim224
git checkout test-kapo-task-sim224
```
Pull to your current branch for depend task:
```php
// git pull upstream  pull/<pull request id>/head
git pull upstream pull/12/head
```
