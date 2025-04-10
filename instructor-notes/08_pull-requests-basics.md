# Instructor Notes: Pull Requests Basics

This document provides instructions for teaching how to create a pull request and merge it into the main branch.
This is a follow-up to the previous instructor notes on working with branches, and it assumes that the participants have already created and pushed their feature branches.

## Learning goals

At the end of this activity, workshop attendees should be able to:

* Understand the concept of pull requests and why we use them
* Understand why small, focused pull requests are better than large ones
* Create a pull request from a feature branch to the main branch
* Merge a pull request into the main branch

## Before demonstration

Before the live demo, slides will introduce the following concepts:

* Pull requests as a way to propose changes to a repository
* Briefly explain what code review is
* The value of small, focused pull requests

In the most recent session, participants will have created two branches:

* `add-renv` branch, which contains:
  * `renv.lock`
  * `renv`-created support files
* `add-fastp` branch, which contains:
  * `environment.yml`
  * modified `download-fastq.sh` script

## Activity

### Altering `download-fastq.sh`

* Checkout the `add-renv` branch locally.
* We will make a small change to `download-fastq.sh` to skip downloading the `fastq` files if they already exist.
  * Check if files exist using the `-e` flag as outlined in [`solutions/fileexists_download-fastq.sh`](solutions/fileexists_download-fastq.sh).
  This sets us up to have a merge conflict with the `add-fastp` branch in the next session.
* Commit the change to the `add-renv` branch.
* Push the changes to the remote `add-renv` branch.
* Instruct participants to navigate to their remote repositories in the browser to see their new commit pushed.
  * Point out the banner that says changes were recently pushed to the `add-renv` branch.

### Protecting `main`

* Navigate to the settings of the repository, where you will demonstrate how to protect the `main` branch.
* In the left sidebar, click on "Branches".
* Under "Branch protection rules", click on "Add branch ruleset".
  * Stress that protecting the `main` branch when working in their own repositories is not practical, and that participants should not follow along in setting this up in their fork.
  The reason why: If you want to keep your `main` branch up-to-date with the upstream repository, you will need to merge changes from the upstream `main` branch into your own `main` branch.
  This is painful to do if your `main` branch is protected.
* Name the ruleset "Protect the default branch."
* Set enforcement status to "Active".
* Show the options for adding a bypass for administrators, but do not select it, and explain that this might lead an administrator to accidentally push to `main`.
* Add the default branch as the branch to protect under "Target branches."
  State that you could also use "Include by pattern" to protect all branches that include `main`.
* Under branch rules, make sure the following are selected:
  * Restrict deletions
  * Require a pull request before merging
    * Require 1 approval
  * Block force pushes
* Hit "Create" to create the branch protection ruleset.
* Show how to edit the ruleset by clicking Rulesets under Rules, and then the ruleset name.

### Creating a pull request

* Instruct participants to create a pull request from the `add-renv` branch to the `main` branch.
  * They will merging their own pull request without requesting a reviewer.
* Scroll down to show the files changed.
* In the pull request title, ask participants to describe the changes in `add-renv` branch at a high-level.
* In the pull request description, ask participants to include a brief summary of the changes made in the `add-renv` branch.
  * Make sure to reference the issue number for the `renv` addition.
  * Note that, by default, participants' forks will not have issues enabled, so their repository will look different from the one in the demo.
* Point out that merging is blocked in the repository the instructor is using because the `main` branch is protected.
* Request a review from the other instructor's GitHub account (you may be requesting your own account depending on computer setup).
  * The other instructor should quickly approve the pull request (which may be you on a second device, such as an iPad or phone).
* Show the conversation, commit, and files changed tabs while waiting for the review.
* Merge the pull request into the `main` branch.
  * Instruct participants to merge their pull request into their own `main` branch without review.
* Instruct participants to delete the `add-renv` branch after merging.
* Instruct participants to pull the changes from the `main` branch into their local repository.
