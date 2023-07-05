# git-workflow
This is a recommended git workflow for project 1. 

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
