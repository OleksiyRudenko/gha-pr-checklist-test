# GitHub Action Recipe - PR Checklist testing

A repo to test auto-commenting GitHub action recipe.
The recipe adds a pre-defined checklist upon labeling a PR, based on a label value.

## Use case

As a repo maintainer I want to 
(GOAL:) have a relevant checklist added as a comment to a PR's conversation
(TRIGGER:) when an eligible label added to the PR that targets specific branches
(ENABLE:) so that the PR opener and/or project maintainers
could check if the contribution matches requirements
and adjust it accordingly.

## Test cases

### Pre-requisites:
- PR checklist files (Checklists) are installed
- required labels (Eligible Labels) are set up
- eligible target branches (Eligible Branches) are defined
- GitHub action `pr-labeled-checklist` (Action) is installed and configured

### Test P1. Happy path to the targeted use case

1. User creates a PR targeted at an Eligible Branch
1. User adds an Eligible Label
1. Action gets triggered

**Desired outcome:** Relevant Checklist added as a comment to the PR's conversation

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
