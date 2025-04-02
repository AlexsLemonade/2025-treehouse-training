# PR review live demonstration


## Before demonstration

Before the live demo, the co-instructor (i.e., instructor who is _not_ leading the demo) will have opened a pull request that adds `fastp` processing to the `download-fastq.sh` script and adds a conda environment file.

Importantly, the `environment.yml` file will contain build numbers, as it will have been created with `conda env export > environment.yml`.
It will also contain a `prefix:` line, which is not needed and includes a hard-coded path.


## Live demonstration

* Navigate to the open pull request and discuss review at a high level:
  * Read through the PR, which links the issue, and discuss how a well-crafted PR can support review
  * Show the Files Changed tab, different views of diffs, and hiding files you have already reviewed to reduce clutter
  * Show views of individual commits, and note that commit messages are helpful for review
* Begin reviewing within GitHub, leaving the following comments for review:
  * Line level comment (download-fastq.sh): suggest adding an explicit output file for the JSON report from `fastp`.
    * Without the report specified, `fastp` will by default create a `fastp.json` report in the current working directory, which may not be where the user expects it to be.
    * Suggest adding the following argument to the `fastp` command (don't forget to add the `\` line continuation character on the previous line):
    ```
    --json "$REPORTS_DIR/${STUDY_ID}_report.json"
    ```
  * File-level comment (environment.yml): The `environment.yml` file should not include build numbers, as this can cause problems with reproducibility
    * Suggest using `conda env export --no-builds > environment.yml` instead
  * Line level comment (environment.yml): suggest removing the `prefix:` line from the `environment.yml` file, as it is not needed and includes a hard-coded path
* Leave overall review starting with some form of "Thanks for doing this!"
  * Include the following overall comments:
    * Note that the usage of the `environment.yml` file is not described in the README for the repo.
    * Suggest adding a section to the README that describes how to set up the conda and renv environments.
    * Note that this could be done in a separate PR, but the issue should be filed before finishing this PR.
* Publish review as "Comment," but discuss consequences if "Request changes" were used instead.
