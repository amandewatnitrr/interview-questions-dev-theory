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

- In Git, the `Index` (also called as the “Staging Area”) is a place where changes are temporarily stored before committing them to the repository.
- It permits you to select and prepare specific alterations from your working directory before properly saving them as part of the project’s history.

### How do you change the last commit in git?

- To change the preceding commit in Git, use `git commit –amend` after making changes, stage them with `git add` , and save with the editor.

### `git checkout`

- `git checkout` helps you switch between branches or return files to a previous state in Git.
- Now, it is suggested to use ‘git switch’ for changing branches and ‘git restore’ to return files.
- Example:
  
  ```bash
  git checkout branch_name # Switches to the branch_name or creates a new branch.
  git checkout -b new_branch_name # Creates a new branch and switches to it.
  git checkout -b new_branch old_branch # Creates a new branch from old_branch and switches to it.
  git checkout file_name # Returns the file to the previous state.
  ```

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

### Difference b/w `reverting` and `resetting`

- `git revert` undos a commit by creating a new commit.
- Example:
  
  ```bash
  git revert HEAD # Reverts the last commit.
  git revert HEAD~2 # Reverts the last 2 commits.
  ```

- `git reset` undos changes by moving the HEAD and branch pointers to a previous commit.
- Example:
  
  ```bash
  git reset HEAD~1 # Resets the HEAD to the last commit.
  git reset --hard HEAD~1 # Resets the HEAD to the last commit and removes all the changes.
  ```

### Difference b/w `git reflog` and `git log`

- `git reflog`

  - `git reflog` shows a log of changes to the HEAD reference.
  - permits you to see the history of changes to the HEAD reference, even if you have changed branches or commits.
  - effective for recovering lost commits or branches that are no longer visible in the `git log`.

- `git log`

  - `git log` shows history of commits made in the repository.
  - lists out commits in linear order.

### What is `HEAD` in Git ??

- `HEAD` is a reference to the last commit in the currently checked-out branch.
- shows the recent commit in the current branch.

### What is purpose of `git tag -a` ??

- `git tag -a` is used to create an annotated tag in Git.
- Annotated tags are tags that contain additional metadata such as the tagger’s name, email, date, and a message. 
- They are valuable for labeling important points in history, like releases, and give another context compared to lightweight tags made with `git tag`.

### What is `Working tree` in Git ??

- The working tree is the directory where you are currently working or modifying.

### What language is used in git ??

- Git is written in C language.
- It's Data structures and algorithms are written in C.

### What is `git diff` ??

- `git diff` is command used to present the difference b/w the working directory, staging area, and the last commit.


### What is Git Object Model ??

- There are 4 objects in Git Object Model:
  
  - `Blob` - It stores the file data.
  - `Tree` - It stores the file structure.
  - `Commit` - It stores the commit object.
  - `Tag` - It stores the tag object.

### How does Git store data ??

- Git stores data by saving snapshots of the project over time.
- Each snapshot is a commit, which covers information about blobs and trees.
- These snapshots are identified by unique hashes, creating it easy to track changes and retrieve history.

### What is meant by `detached HEAD` in Git ??

- `Detached HEAD` is a state in Git where the HEAD points to a commit instead of a branch.
- Changes made in this state are not attached to any branch, and can be lost if not saved.

### What is `git cherry-pick` ??

- `git cherry-pick` is a command used to apply a commit from one branch to another.
- It is useful when you want to apply a single commit from one branch to another.
- Example:
  
  ```bash
  git cherry-pick commit_hash # Applies the commit with commit_hash to the current branch.
  ```

- But, be careful while using this command, as it can lead to conflicts.
- Also, it's very complex to use this command in case of merge commits.
- It's better to use `git rebase` in such cases.