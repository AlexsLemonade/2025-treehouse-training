# Instructor Notes: Project management with `renv`, and using feature branches

This overall activity relies broadly on two new concepts: i) using `renv` to manage R projects, and ii) branching and merging.
This document provides instructions for teaching how to create and push to a feature branch, and subsequently merge into main.
The feature branch of interest here should contain a `renv.lock` file and other renv-related files from `renv` setup.

## Learning goals

At the end of this activity, workshop attendees should be able to:

* Understand how to use `renv` to manage R package versions in R projects
* Understand the concept of `git` branches and how to make them
* Understand the concept of `git` merging and how to perform it within a given repository (not across forks)
  * Merge conflicts will _not_ be covered in depth, but we will mention it


## Activity

### Part 1: `renv` and `conda`

Begin with the "Managing packages and environments" slides to introduce `renv` and `conda`.

#### renv setup demonstration

* Interactively demonstrate to trainees how to set up renv for their project using `renv::init()`.
* Show the created files, including `renv.lock`, updates to `.Rprofile`, and contents of the `renv` directory.
* Possibly note that `renv` adds its own `.gitignore` file!

#### conda setup demonstration

* Create a new environment named `alsf-rrp` with `fastp` installed using `conda create -n alsf-rrp fastp`.
* Show how to activate the environment with `conda activate alsf-rrp`.
* Save the conda environment with `conda env export > environment.yml`.
* (Optional) Add FastQC to the environment with `conda install fastqc` and export again.
* Show how to deactivate the environment with `conda deactivate`.

### Add fastp to the download-fastq.sh script

* Add trimmed and reports directories to the `download-fastq.sh` script and update the `mkdir -p` command to create these directories.

```bash
TRIMMED_DIR="../data/trimmed/${STUDY_ID}"
REPORTS_DIR="../reports/fastp"

mkdir -p $FASTQ_DEST $TRIMMED_DIR $REPORTS_DIR
```

* Modify the file download blocks to only download the fastq files if they are not already present.
**Use the `-f` flag to check for the existence of each file.**

```bash
if [ ! -f "$FASTQ_DEST/$FASTQ_R1" ]; then
    ...
fi
```

* Add the fastp command to the script:
*
```bash
## Trim the files with fastp
fastp \
  --in1 $FASTQ_DEST/$FASTQ_R1 \
  --in2 $FASTQ_DEST/$FASTQ_R2 \
  --out1 $TRIMMED_DIR/$FASTQ_R1 \
  --out2 $TRIMMED_DIR/$FASTQ_R2 \
  --html "$REPORTS_DIR/${STUDY_ID}_report.html" \
  --json "$REPORTS_DIR/${STUDY_ID}_report.json"
```

* Run the script to ensure that it works (and doesn't re-download the files).


* Trainees should now all have a `renv.lock` file and other renv-related changes in their _main branch_.
**Do not stage/commit/push any of these changes yet!**

### Part 2: Branches and merging

* At this time, transition to the "Branch" slides to introduce the concepts of branching and merging.
* After the slides, interactively demonstrate how to create a new branch, which should be called something like `add-renv`.
* Trainees should then stage/commit/push the `renv` files to a remote branch, which will be created during the `push`.
* GitKraken should now show diverged histories between `main` and `add-renv`.

* Instruct trainees to navigate to their remote repositories in the browser to see their new branch pushed.
* In particular, make sure trainees see the github message along the lines of "This branch 1 commit behind the main branch" inside the `add-renv` branch view.
* Return to GitKraken to _merge_ this feature branch into their `main` branch, push to `main`, and then delete the remote (and the local if preferred!) `add-renv` branch.
  * Reiterate point from slides that other types of project workflows might not directly merge branches into `main`
* Finally, if the local branch was not deleted, ensure trainees end up in their `main` branch locally.
