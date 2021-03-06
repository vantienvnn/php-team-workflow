Git process workflow
=====================

Please following our GIT convention requirement:

- Fork project repository to your GitHub account
- Make sure you do not push, merge to project repository
- Create one branch for each your tasks on JIRA (*)
  - Checkout from test branch for fix bug issues
  - Checkout from develop branch for new feature issues
- Make sure end of text files (css, js, php ...) will have one black line
- When you do finished your task:
  - Rebase your branch from branch has checkout (see *) in Project Repository
  - Make sure one commit for one Pull Request ( PR )
  - Create a PR on Github in your repostiory to branch has checkout (see *) of project repository
  - Name of PR should have issues ID in Jra
    for example: Implement SIM-1293
- When you do created your PR:
  - If have conflict message form Github you are forgot rebase
  - You can pick other task on waiting Simble CI checking your PR, move this task to impediment
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
If Id of your task on JIRA are SIM-201, so you should create a branch like as:
```php
// checkout to test branch first
git checkout test
// create new branch
git checkout -b SIM-201
// Rebase upstream test before do anything
git fetch --all
git rebase upstream/test
```

How about have one commit for PR?
=====================
For the first commit:
```php
git add .
git commit -m "Implement task SIM-201"
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

How to rebase your branch?
=====================
(This function will keep your local branch are updated with project branch)

Please make sure your are added upstream as above document
```php
git fetch --all
git rebase upstream/test
// if not have conflict
git push origin <branch-name> -f
```
If you have conflict in rebase process
- You can't not use git checkout command if don't know it
- Resolve the conflict files
- When you have resolved all conflict files:
```php
git add .
git rebase --continue
git push origin <branch-name> -f
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

Pull to your current branch for testing PR (this command will deleted your change):
```php
// git pull upstream  pull/<pull request id>/head -X theirs
git pull upstream pull/12/head -X theirs
```

What Simble CI
=====================
Simble CI is a tool for auto check your PR, so when Simble CI will run test for you PR?
- You are create a new PR
- When you push new/amend commits in branch of PR to your repository
  So, Just re-update (push) your branch when you have test you code are fixed all errors

What is Simble CI status?
- Your PR test result is succeed
 ![Settings Window](https://raw.github.com/vantienvnn/php-team-workflow/master/images/simble-ci-ok.PNG)
- Your PR test result is failed
 ![Settings Window](https://raw.github.com/vantienvnn/php-team-workflow/master/images/simble-ci-fail.PNG)

How to check error message in Simble CI?
- Click details link in Simble CI status
- Login to Simble CI system
- Click console menu in left sidebar of Simble CI

Other Tips:
=====================
- How to dectect missing new line in end of file?
 ![Settings Window](https://raw.github.com/vantienvnn/php-team-workflow/master/images/missing_newline.PNG)
- How to keep your code is safe on rebase?
  - Don't commit --amend to another guys commit
  - Review your PR code after rebase
  - Check other guys PR for sure they don't change your code
