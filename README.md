# git-workflow
This is a recommended git workflow for projects
the best pratices are:
1. add a .gitignore file when create the project on github
2. communicate with your team
3. divide work into files, classes, functions to reduce conflicts.

## Step 1. Pull the latest code from the main branch:
Before starting work on a new feature, each team member should update their local main branch to match the main branch in the remote GitHub repository. You can then create a new branch off of main for your feature. This helps ensure that everyone is starting from the most recent code.

### git checkout main
### git pull origin main
### git checkout -b your-feature-branch

## Step 2. Work on the feature and commit changes:
As you make changes for your feature, you should regularly commit those changes to your feature branch. Regular commits help track progress and make it easier to identify and fix issues.

### git add .
### git commit -m "Description of changes made"

## Step 3. Pull the latest code from main and merge into the feature branch:
Before pushing your feature branch to GitHub, it can be helpful to pull the latest code from main and merge it into your feature branch. This can help catch and resolve any merge conflicts before the changes are pushed to GitHub. If there are conflicts, you need to resolve those conflicts.

Method 1:
### git checkout main
### git pull origin main
### git checkout your-feature-branch
### git merge main
Method 2:
### git checkout your-feature-branch
### git pull origin main

## Step 4. Push the feature branch to GitHub:
git push origin your-feature-branch

## Step 5. Create a Pull Request on GitHub:
The github manager then creates a pull request on GitHub to merge the feature branch into main. Team members can review the changes, suggest modifications, and eventually approve the pull request.

## Step 6. Once the pull request is approved, it can be merged into main on GitHub.

## Step 7. Pull the latest code from main:
After the pull request is merged, all team members should pull the latest code from main to their local main branch to stay up-to-date with the combined changes.
### git checkout main
### git pull origin main

By following this process, all the teammates can work simultaneously on different features while ensuring you are all working with the most updated code and that your changes don't conflict with each other.

## How to resolve merge conflicts:
https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line

## How to reduce conflicts. 
You should create .gitignore file and add ".ipynb_checkpoints" directory to the ".gitignore" file

[An Example of .gitignore]https://github.com/softmaxhuanchen/git-workflow/blob/main/.gitignore

## How to remove ".ipynb_checkpoints" from your main branch on github.
### Step 1. 
### git rm -r --cached .ipynb_checkpoints
This command removes the .ipynb_checkpoints directory from the Git repository (the --cached option ensures the actual files remain on your disk). If your checkpoint files are in another directory, you may need to adjust the path accordingly.
### Step 2. 
### git commit -m "Remove .ipynb_checkpoints"
### git push origin main
This will commit the changes and push them to the main branch on your remote repository.
### Step 3. Update .gitignore: Lastly, to prevent these files from being added to the repository in the future, you should add .ipynb_checkpoints to your .gitignore file. 
### Step 4. commit and push the .gitignore file to your repository
### git add .gitignore
### git commit -m "Add .gitignore"
### git push origin main

## If git hangs when pushing to github try to increase the buffer:
### git config --global http.postBuffer 524288000

## Understanding conflicts and how to handle them
Here are 3 situitions:  
1. Local Ahead of Remote:
If you have more commits locally than on the remote, then you are "ahead" of the remote.
In this case, a simple git push will update the remote branch to match your local branch.

2. Remote Ahead of Local:
If the remote has more commits than your local branch, then you are "behind" the remote.
Here, a git pull (which is essentially a git fetch followed by a git merge) will fetch the new commits from the remote and merge them into your local branch, bringing you up-to-date.

3. Divergent Branches:
This is where both the local and remote branches have new commits that the other doesn't have. The branches have "diverged."
A simple git push won't work here because the histories are different and Git doesn't want to risk losing any commits.
When you do a git pull, Git will try to merge the remote changes into your local branch. This might lead to merge conflicts if the same parts of the code were changed in both your local commits and the new remote commits.
You'll need to decide how to reconcile the differences, typically through either a merge or a rebase:
Merge: This will create a new merge commit in your local branch that has two parents: the last local commit and the last remote commit. It's a way to tie the two histories together.
Rebase: This takes your local changes and "replays" them on top of the remote changes, making it look as if you made your changes after the latest remote changes. This can provide a cleaner, linear commit history but might be a bit more complex to handle, especially if there are many conflicts.

4. Handling Divergent Branches:
If you've identified a specific file that's causing the divergence and you're in the middle of a merge (or rebase) conflict, you can use git checkout with the --theirs or --ours options to choose a specific version of that file.

   i. If you decide the remote version of the file is the correct one and you want to discard your local changes for that particular file:
   git checkout --theirs path/to/conflicted_file.ext
   ii. If you believe your local changes are the correct ones and want to discard the changes from the remote for that file:
   git checkout --ours path/to/conflicted_file.ext
   iii. After choosing a version, you should mark the conflict as resolved by adding the file to the index:
   git add path/to/conflicted_file.ext

6. If you want to discard your local commits and make your local branch exactly match the remote branch, follow these steps:
   1) Fetch the Latest Remote Changes: git fetch origin
   2) Reset Your Local Branch: git reset --hard origin/main (Use the reset command with the --hard flag to set your current branch's HEAD to the specified commit (in this case, the latest    commit of the remote branch).
   3) Clean Up Untracked Files (Optional):git clean -fd
      -f: Stands for "force", which is required when using git clean.
      -d: Removes untracked directories in addition to untracked files.
   4) After performing these steps, your local branch will match the state of the remote branch, and all local commits that were divergent will be discarded. Remember to be careful with       these commands, especially reset --hard, as it discards commits and there's no simple undo. Always make sure you're okay with losing changes before using it.


