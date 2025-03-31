# Instructor Notes: Working with Git Branches

This document provides instructions for teaching how to create and push to a feature branch.
As we are going to show merging first in the context of a pull request, there will be no merges in this part of the demo.


## Learning goals

At the end of this activity, workshop attendees should be able to:

* Understand the concept of `git` branches and how to make them
* Manange more than one branch with independent sets of changes
* Cherry-pick commits from one branch to another, and revert commits

## Before demonstration

Before the live demo, slides will introduce the follow concepts/commands:

* Exploring project history in GitHub using `scpca-nf`
  * See past commits, releases and/or tags
  * `Blame` view (use [`scpca-nf/bin/post_process_sce.R`](https://github.com/AlexsLemonade/scpca-nf/blob/main/bin/post_process_sce.R), a script with three contributors)
* Introduce feature branches conceptually and why we use them, including informative branch names
  * Note that more discussion of feature branches will come later in the afternoon during git workflow slides
* Introduce `git merge` and (why not to use) `git rebase`
* Introduce `git checkout` (as in `git switch`) and `git branch`
* Introduce `git stash` and `git cherry-pick`



## Activity

### Creating a single branch

* After the Git part 2 slides, we will demonstrate how to create a new branch, which should be called something like `add-renv`.
* Trainees should then stage/commit/push the `renv` files to a remote branch, which will be created during the `push`.
* "Accidentally" include the `environment.yml` file as a second (or third) commit.
* GitKraken should now show diverged histories between `main` and `add-renv`.
* Instruct trainees to navigate to their remote repositories in the browser to see their new branch pushed.
  * In particular, make sure trainees see the github message along the lines of "This branch is 2 commits ahead of main" inside the `add-renv` branch view.
  * Point out the pull request button, but do not click it yet.

### Creating the second branch

* Now return to GitKraken to create a separate branch for adding the conda environment.
* Create a branch off of `main` named `add-fastp`.
* Make a commit to add the changes to the `download-fastq.sh` script to use `fastp`.
* "Realize" that the `environment.yml` addition should really be in this branch, and not in `add-renv`.
  * Cherry pick the `environment.yml` comit from `add-renv` to `add-conda`.
* Push changes in `add-fastp` to remote
* Check out the `add-renv` branch, revert the commit with `environment.yml` and push the changes to the remote.

Following these steps, trainees should have two branches with the following changes:
* `add-renv` branch:
  * `renv.lock`
  * `renv`-created support files
* `add-fastp` branch:
  * `environment.yml`
  * modified `download-fastq.sh` script

Nothing has been merged to main, because we will do that through pull requests in the next steps.
