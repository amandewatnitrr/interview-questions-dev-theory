# React.Js Interview Questions

### What is Git ?

- Git is a distributed version control system that is used to track changes in source code during software development.
- It permits multiple developers to work on a project together without interrupting each other’s changes.
- Git is especially popular for its speed, and ability to manage both small and large projects capably.

### What is `origin` in Git ?

- “origin” states to the default name offered to the remote repository from which local repository was cloned.
- It is used as a reference to control fetches, pulls, and pushes.

### What is purpose of `.gitignore` file ?

- The `.gitignore` file is used to specify files and directories that should be ignored by Git.
- It is used to avoid attaching unneeded files (like logs, temporary files, or compiled code) to your repository. 
- This saves repository clean and targeted on important files only.

### What is Version Control System ??

- A version control system (VCS) records the work of developers coordinating on projects. 
- It keeps the history of code changes, permitting developers to add new code, fix bugs, and run tests securely. 
- If required, they can restore a past working version, verifying project security.

### `git push`

- `git push` is a Git command used to upload local repository content to a remote repository.

### `git pull`

- `git pull` is a Git command used to fetch and download content from a remote repository and immediately update the local repository to match that content.

### What is `commit` in Git ??

- A commit is a snapshot of changes made to the project at a specific point in time.
- It grabs all the changes you have made to files—like additions, or deletions of files at a particular moment.
- Each commit has a unique message explaining what was done.
- This helps you track your project’s history, undo changes if requisite, and work with others on the same project.

### Conflict in Git

- Git usually manages merges automatically, but conflicts occur when two branches edit the same line or when one branch deletes a file that another edits.

### What is index in Git ??

- In Git, the “Index” (also called as the “Staging Area”) is a place where changes are temporarily stored before committing them to the repository.
- It permits you to select and prepare specific alterations from your working directory before properly saving them as part of the project’s history.

### How do you change the last commit in git?

- To change the preceding commit in Git, use `git commit –amend` after making changes, stage them with `git add` , and save with the editor.

### `git checkout`

- `git checkout` helps you switch between branches or return files to a previous state in Git.
- Now, it is suggested to use ‘git switch’ for changing branches and ‘git restore’ to return files.

### Difference b/w `git fetch` and `git pull`

- `git fetch`

  - It fetches updates from a remote repository but does not combine them into your local repository.

  - It fetches all the new data from the remote repository that you don’t have yet, but it stores it in a separate area, permitting you to review the changes before merging them into your working directory.

- `git pull`

  - fetches the updates from the remote repository and instantly strives to merge them into your current branch.
  - It is basically a union of `git fetch` followed by `git merge`.

### Explain `git rebase`

- `git rebase` is a process to combine changes from one branch to another.
- It helps in forming a linear history, avoiding merge commits.
- Example:
  
  ```bash
  git checkout branch_name
  git rebase main # This command takes the changes on feature temporarily stores them, and then applies them on main.
  # Resolve any Conflicts that might be there.
  # Once the conflicts are resolved
  git add .
  git rebase --continue # After resolving all the conflicts continue the rebase.
  # If you have already push the "branch_name" to the remote repository, you will have to force push it, to overwrtie the history.
  git push --force-with-lease origin branch_name
  ```

### Difference b/w `git clone` and `git remote`

- `git clone` downloads the copy of the remote repository on the local repository, including all the git history.
- `git remote` controls connections to remote repositories. It sets up links to remote repositories but does not download the repository.

### `git stash`

- `git stash` command is used to temporarily save and revert changes in the working git directory, that are not yet ready to be committed.
- Example:
  
  ```bash
  git stash # Stashes the changes
  git stash list # Lists all the stashes
  git stash pop # Applies the last stash, and removes it from the list.
  git stash apply # Applies the last stash, but does not remove it from the list.
  git stash apply stash@{1} # Applies the stash at index 1.
  git stash clear # Removes all the stashes.

  ```