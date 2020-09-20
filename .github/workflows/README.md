BSSw Workflows

This file is intended to provide a roadmap to the various workflows.  Further comments should be found within each file.

Format:
* Filename (name)
    - trigger(s)
    - jobname
        - description

# Workflows in use
* merge-master-to-preview.yml (Sync master to preview)
    - trigger: push to master branch
    - job: sync-preview
        - Merges from master into preview branch.
* merge-pr-to-preview.yml (Sync pull request to preview)
    - trigger: pull request [opened, synchronized] on master branch
    - job: sync-pull-request
        - Merges PR into preview branch
* no-prs-on-preview.yml (Reject pull requests on preview branch)
    - trigger: pull request [opened, reopened] on preview branch
    - job: reject-pr
        - Attempts to open a PR against the preview branch are immediately closed and an explanatory comment is added to the PR.

# Gaps
* PR is closed without merge.  We should back out the whole PR from preview.
* Recreate preview branch.  Trigger manually
    - Delete preview
    - Create preview from master
    - Foreach open PR
        - Merge PR to preview
* Have not investigated possibilities for conflicts and how they should be handled.
* Quality checks on content
    - verify links
    - check spelling
    - markdown lint (are we too different for this to be useful?)
    - BSSw required elements
    - verify BSSw metadata
    - BSSw style

# Potentially useful actions
* ljharb/require-allow-edits
    - I think it would probably be nicer to *suggest* rather than require
* mschilde/auto-label-merge-conflicts
    - On push, check all outstanding PRs for merge conflicts.  Add label and comment.
* outsideris/potential-conflicts-checker-action
    - On PR update, compare against all outstanding PRs for possible conflicts and add comments
