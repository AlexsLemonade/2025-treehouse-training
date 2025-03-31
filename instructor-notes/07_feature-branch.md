# Instructor Notes: Project management with `renv`, and using feature branches

This document provides instructions for teaching how to create and push to a feature branch, and subsequently merge into main.
The feature branch of interest here should contain a `renv.lock` file and other renv-related files from `renv` setup.

## Learning goals

At the end of this activity, workshop attendees should be able to:

* Understand the concept of `git` branches and how to make them
* Understand the concept of `git` merging and how to perform it within a given repository (not across forks)
  * Merge conflicts will _not_ be covered in depth, but we will mention it


## Activity


* At this time, transition to the "Branch" slides to introduce the concepts of branching and merging.
* After the slides, interactively demonstrate how to create a new branch, which should be called something like `add-renv`.
* Trainees should then stage/commit/push the `renv` files to a remote branch, which will be created during the `push`.
* GitKraken should now show diverged histories between `main` and `add-renv`.

* Instruct trainees to navigate to their remote repositories in the browser to see their new branch pushed.
* In particular, make sure trainees see the github message along the lines of "This branch 1 commit behind the main branch" inside the `add-renv` branch view.
* Return to GitKraken to _merge_ this feature branch into their `main` branch, push to `main`, and then delete the remote (and the local if preferred!) `add-renv` branch.
  * Reiterate point from slides that other types of project workflows might not directly merge branches into `main`
* Finally, if the local branch was not deleted, ensure trainees end up in their `main` branch locally.
