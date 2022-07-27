# PR Labeled Checklist - A GitHub Action Recipe (ghar)

A GitHub Action Recipe that adds a pre-defined checklist
upon labeling a PR, based on a label value.

Version 0.9

## Use case

As a repo maintainer I want to 
(GOAL:) add a relevant checklist as a comment to a PR's conversation
(CONDITION:) when an eligible label added to the PR that targets specific branches
(ENABLE:) so that the PR opener and/or project maintainers
could check if the contribution matches requirements
and adjust it accordingly.

## How to use

On a targeted repo:
1. Create labels that you will use to trigger the action (Eligible Labels).
   It is recommended to use dashes or underscores instead of spaces.
   Examples: `staging-deployment`, `dry_run`
1. Create checklists, one per each label, where each checklist filename matches an Eligibale Label name.
   Examples: `staging-deployment.md`, `dry_run.md`
   Recommended (default) path to checklists is `.github/pr-checklists/`.
1. Copy the [pr-labeled-checklist workflow](.github/workflows/pr-labeled-checklist.yml) and edit it as appropriate
1. Test your setup to make sure it works as expected

> **NB!** You will want to have your collaborators' fork contain the latest
> versions of the workflow and templates on their forks' source branches as
> these (and not the versions on the targeted repo and branch) are used by GitHub actions engine.

## Test cases

### Pre-requisites:
- PR checklist files (Checklists) are defined
- required labels (Eligible Labels) are set up
- eligible target branches (Eligible Branches) are defined
- GitHub action `pr-labeled-checklist` (Action) is created and configured

### Test P1. Happy path on a local PR

1. User creates a PR targeted at an Eligible Branch from a branch on the same repo
1. User adds an Eligible Label
1. Action gets triggered

**Desired outcome:** Relevant Checklist added as a comment to the PR's conversation

### Test P2. Happy path on a PR from a fork

1. User creates a PR targeted at an Eligible Branch from a forked repo
1. User adds an Eligible Label
1. Action gets triggered

**Desired outcome:** Relevant Checklist added as a comment to the PR's conversation

### Test P3. Happy path with multiple checklists

1. User **starts opening** a PR targeted at an Eligible Branch from a branch on the same repo
1. User adds 2 or more Eligible Labels and creates a PR
1. Action gets triggered

**Desired outcome:** Relevant Checklists added as comments to the PR's conversation
one per each Eligible Label

### Test N1. PR doesn't target an Eligible Branch

1. User creates a PR targeted at a branch that is **not** an Eligible Branch
1. User adds a label that is an Eligible Label
1. Action gets triggered

**Desired outcome:** No Checklists added

### Test N2. PR labeled with a label that is not an Eligible Label

1. User creates a PR targeted at an Eligible Branch
1. User adds a label that is **not** an Eligible Label
1. Action gets triggered

**Desired outcome:** No Checklists added
