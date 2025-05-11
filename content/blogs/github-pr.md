+++
date = '2019-08-08T02:37:14+05:30'
draft = false
title = 'GitHub PR'
+++

This will guide you through making a pull request to a GitHub repository through the terminal so that you can make your life easier while working on a project.

### How it works:
1. A developer creates the feature in a dedicated branch in their local repo.
2. The developer pushes the branch to a public GitHub repository.
3. The developer files a pull request
4. The rest of the team reviews the code, discusses it, and alters it.
5. The project maintainer merges the feature into the official repository and closes the pull request.

### Fork a Repository:
To create a pull request you need to have made your code changes on a separate branch on the forked repository. To fork a repository you need to open the repository and click on the fork button. You'll get a copy of the repository after fork. 

### Clone the Repository:
To make your own local copy of the repository you would like to contribute to, let's fire up the terminal.
We'll use `git clone` command with the URL that points to your fork of the repository.

```bash
$  git clone https://github.com/username/repository.git
```

### Create a New Branch:
This is where you'll add your features. If you create a new file remember to add it with git add command and commit them.

```bash
$  git add [file-name]
$  git commit -m "commit message"
```
At this point you can push your changes to the new branch of your forked repository.

```bash
$  git push origin [new-branch]
```

### Make the Pull Request:

This is the most simple step if till now you've done correctly. Now click on the New pull request button in your forked repo. Write down a nice report explaining why these changes should be included in the official source of your project and then confirm. Project author will get a notification that you submitted a PR. They will review your code and you'll get notification for their further actions. They may reject your PR or they may suggest something for changes. Go back, edit it and push again. PR will be automatically updated. If the maintainer is want to integrate your contributions to the project, the maintainer have to click Merge and your code will become a part of the original repo.


