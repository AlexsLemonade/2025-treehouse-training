# Dealing with merge conflicts


## Before demonstration

When we get to this point, the `add-renv` branch has been merged into `main` (and probably deleted).
This should have included a change in teh `download-files.sh` script to check if the fastq files already exist before downloading them.
The `add-fastp` branch has changes to `download-files.sh` and `environment.yml`.

Repeat that is good practice to merge the base branch into your feature branch before filing a PR.
We will be merging the `main` branch into the `add-fastp` branch, which will result in a merge conflict in `download-files.sh`.

## Live Demo

* In GitKraken, check out the `add-fastp` branch and run `git merge main` (or the GitKraken equivalent).
* This should result in a merge conflict in `download-files.sh` where one version uses the `-e` flag to check if the files exist and the other uses the `-f` flag.
  * Show the indications that there is a merge conflict in GitKraken.
* Open the conflicted file in VS Code and show the conflict markers.
  * Show how to resolve the first conflict by manually removing the conflict markers and keeping the desired code.
* Go back to GitKraken and show the conflict view.
  * Show how to resolve the conflict by selecting individual lines of code (as well as options to include all changes from one file or the other).
* Save the changes and commit the merge.
* Push the changes to the remote `add-fastp` branch.


### Final punchlines of demo

* Sync up with your base branch sooner rather than later
* Don't let branches/PRs get too stale, as they will get increasingly out of sync
* Coordinate with your team to reduce odds of working on the same lines of code at once



