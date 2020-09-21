# git

## On Commits

Try to keep each commit message concise, relevant, and _release-notes-ready_:
- Leverage the **first line** as the **subject**, try to confine it within 50 characters long. This part should be usable for release notes.
- Clearly specify if the commit contains breaking changes.
- Optionally put **lengthier details** in the message **body**, as bullet points or paragraphs. They should contain all technical details that are valuable for fellow contributors, reviewers and your-future-selves.

Try to keep each commit's code changes as isolated from each other as possible:
- Scope closely coupled code changes within a single commit.
- Special cases such as structural refactors (without feature changes) should live in their own commits, and marked so in the commit messages, instead of mixing with feature alteration code changes.
- On the other hand, when non-impacting minor code changes happen (such as `console.log`, `debug`, etc.), leverage `--amend`, squash (through interactive rebasing), `cherry-pick` (to pick out and/or re-arrange commit order), or all other available git tools into relevant commits, instead of forming their own.

### Feature Change Example

```COMMIT_EDITMSG
# 👍 GOOD
# Title line, release notes ready
Hub - extend Dataset Flow with JSON parsing

# Detail lines, technical for contributors and reviewers
- `FileReader` based JSON parser, with API emulated as Papaparse's
- `Dropzone` usage restrained from multiple files
- Extend column data type inference logic to handle non-string values

# 👎 BAD (lack of main feature, and ambiguous phrasing)
add JSON
```

### No Feature Change Example

```COMMIT_EDITMSG
# 👍 GOOD
Hub - no feature change refactor

- Workflow components rewritten using React hooks
- Hooks factored out to be reusable across different workflows
- Nomenclature changes

# 👎 BAD
refactor
```

### Breaking Change Example

```COMMIT_EDITMSG
# 👍 GOOD
builder (BACKWARD INCOMPAT w/ FO) - v4 POI parameters

# 👍 GOOD (alt, shorter)
builder (BREAK FO) - v4 POI parameters

# 👎 BAD
builder - v4 POI parameters
```

**Tip**: when authoring commit messages, use `git commit -v` to get a comfortable editor environment (of your choice), as well as having the code changes right below for reference.

## On Local Development Branches

Try **NOT** to directly commit to the main branch. Even if you are the sole maintainer now, there is always the possibility of new members joining.

Try to stay up-to-date with the upstream main branch, and also actively perform `git fetch --prune` to clean up idle references.

Perform controlled commit amends, squashes, and cherry-picks as much as needed, to maintain a good commit history (see [`On commits`](#on-commits) section) when pushed to upstream.

Name the branch as `scope/change-title`, or if needed, `scope/sub-scope/change-title` where `scope` depends on convention on a per-project basis. Resist the temptation to bundle out-of-scope commits within it, start new branches for those. If they need to be contiguous to function properly, chain-branch off from the `scope` branch instead of the main branch.

```bash
$ git branch
  hub/dataset-flow
* hub/csv/fix-parsing # contiguously branched off from hub/dataset-flow
  main # the main branch of the repo
```

### Common Pitfall - Accidental `git commit` instead of `git rebase --continue`

An [Q&A on Stackoverflow](https://stackoverflow.com/questions/6457044/forgot-git-rebase-continue-and-did-git-commit-how-to-fix) covers this very case. In short:

```bash
# It moves the HEAD pointer to its parent but keeps the work tree
# and adds the merge change to the index
$ git reset --soft HEAD^

# So you can continue rebasing with
$ git rebase --continue  # as before
```

### Squash Commits

Squash commits with `git rebase -i` (`i` for interactive), which gives more granular control than `git commit --amend`.

Example:
1. `git rebase -i HEAD~3` brings 3 commits from and including `HEAD`:

```bash
pick 6df9b94 has_aoi - add query to check if each poi could be found in aoi report table - if yes/no: response will include has_aoi flag indicating true/false
pick 6d9075c mend
pick 95e9ccd report_vwi - add has_aoi query logic to vwi reports
```
Followed by a series of commands to edit the commits:
```bash
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit
```
2. edit and replace the key word `pick` with `squash` (or `s`):  

Upon saving, git editor will prompt with the view to edit the commit messages:
```bash
# This is a combination of 2 commits.
# This is the 1st commit message:

has_aoi - add query to check if each poi could be found in aoi report table
- if yes/no: response will include has_aoi flag indicating true/false

# This is the commit message #2:

mend
```
Save and exit to complete the squashing.  

3. `git push --force`:  

Run `git status` to confirm your changes:
```bash
On branch report_wi/hasAoiFlag
Your branch and 'origin/report_wi/hasAoiFlag' have diverged,
and have 2 and 3 different commits each, respectively.
```
Run `git push --force` to update your branch.

## On Tags

Try to maintain a tagging practice that suits the project's release cycle. Adopt [semantic versioning](https://semver.org/) wherever possible.

```bash
$ git tag
v1.2.10
v1.2.11
v1.2.11-alpha.0
v1.2.11-alpha.1
v1.2.12
v1.2.7
v1.2.8
v1.2.9
```

This would allow for some nice tricks to automate tedious tasks, such as listing out commits between tags and/or branch HEADs:

```bash
$ git log v1.2.12..HEAD --pretty=oneline --abbrev-commit --author=runzhou.li
c5f91ec Builder/Hub - prevent actions before WL is chosen
7461541 Hub - allow multiple (composite) `primary_key`s
e323208 Hub - deprecate `primary` for `primary_key`
326cc64 Hub - bug fix of ISO date detected as IP, also:
```

Based on this, combined with a good convention [on commits](#on-commits), we can leverage tools like (our own) [release CLI](https://github.com/EQWorks/release) to generate nicely arranged release notes material.

## On Pull/Merge Requests

Try to maintain a good length and depth of the code changes within each request, make it digestible within 30 minutes or less.

Try to keep a [`CHANGELOG`](https://keepachangelog.com)-like summaries of changes in the request description. Try to attach screenshots/videos to demonstrate the workflow and before/after differences. This can be automated/semi-automated through good practices [on commits](#on-commits).

Reference and mark relevant issues as fixed (`fixes #123`), or label the request itself when there are no relevant issues -- not both.

Start the request as a draft and/or mark in the title with `[WIP]` prefix when it needs more time to complete. Mark it ready to review, and/or with a `[G2M]` prefix in the title to signal its readiness.

When reviewer approved the PR, it's ready for merge. Three ways to meget it through GitHub:

#### Create a merge commit
Merge with [`--no-ff` option](https://git-scm.com/docs/git-merge#_fast_forward_merge) -- this gives a good indicator (the merge commit) of the bundling of code change commits. Also, the commit history and its timeline are [fully preserved](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=le).

#### Squash and merge
**TRY NOT TO SQUASH MERGE.**

#### Rebase and merge
The relevant commits are all rewritten to be brought on [top of the `HEAD` of the target branch](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=le). That means the commit history and its timeline _can be_ altered. In return, you gain a full block of commits that represent intended code changes next to each other.

## On Reviewing

Try to set aside some quality time as a routine to proactively review others' pull/merge requests, as thoroughly as your bandwidth allows. If there's no time, and/or no willingness, do not just cast approval without reviewing.

Actively self-review and monitor your own pull/merge requests -- be on the lookout for potential conflicts after other requests have been merged.

When giving code change requests, think twice before you submit -- be reasonable and constructive, and be ready to defend your reasons.

If the code change suggestion does not warrant definitive reasoning, but would still be constructive in your opinion, make it as a non-blocking comment.

Where relevant, go through the changes in deploy preview or in your local environment to check for UI/UX flow as well as bugs.

Prioritize on reviewing those that marked as bug fixes, then the new features. Use `G2M` as a search filter to minimize noise -- provided that it is a well-followed convention in the given project.

## General references

- [GitHub article on merge methods](https://help.github.com/en/articles/about-merge-methods-on-github)
- [Git documentation on merge](https://git-scm.com/docs/git-merge)
- [Atlassian article on Merging vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [VS Code as Git editor](https://code.visualstudio.com/docs/editor/versioncontrol#_vs-code-as-git-editor)
