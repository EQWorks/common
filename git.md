# git

## On Commits

Try to keep each commit message concise, relevant, and _release-notes-ready_:
- Leverage the **first line** as the **subject**. Try to confine it within 50 characters long. Aim to make this part usable for release notes.
- Specify if the commit contains breaking changes.
- Optionally put **lengthier details** in the message **body**, in the form of bullet points or paragraphs. They should contain all technical information that is valuable for fellow contributors, reviewers, and your future selves.

Try to keep each commit's code changes as isolated from each other as possible:
- Scope closely coupled code changes within a single commit.
- Exceptional cases such as structural refactor (without feature changes) should live in standalone commits and be marked accordingly in the commit messages instead of mixing with feature alteration code changes.
- On the other hand, when non-impacting minor code changes happen (such as `console.log`, `debug`, etc.), you can:
  - Squash through interactive rebasing `git rebase -i`
  - Squash the current change into the most recent commit through `git commit --amend`
  - `git cherry-pick` (to pick out or re-arrange commit order)
  - Or other applicable git commands

### Feature Change Example

```COMMIT_EDITMSG
# 👍 GOOD
# Subject title line, concise and informative
Hub - extend Dataset Flow with JSON parsing

# Body detail lines, technical for contributors and reviewers
# Note it's necessary to keep an empty line between the subject and body lines
- `FileReader` based JSON parser, with API emulated as Papaparse's

    const reader = new FileReader()
    reader.onloadend = () => {
      setPreviewURL(reader.result)
    }

- `Dropzone` usage restrained from multiple files
- Extend column data type inference logic to handle non-string values

# 👎 BAD (lack of the main feature and ambiguous phrasing)
add JSON
```

### No Feature Change Example

```COMMIT_EDITMSG
# 👍 GOOD
Hub - no feature change refactor

- Rewrite workflow components using React hooks
- Factor out reusable hooks across different workflows
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

**Tip**: when authoring commit messages, use `git commit -v` to get a comfortable editor environment (of your choice) and have the code changes right below for reference.

### Automated Enforcement

Suppose we adopt the general commit message (subject line) convention `category[/sub-category] - subject title` for a given project repository. In that case, we can leverage our [`commit-watch` CLI](https://github.com/EQWorks/commit-watch) to perform quick checks. It is convenient when integrated into the continuous integration process for pull/merge requests, for example, through GitHub Actions:

```yml
jobs:
  # ...other jobs
  commit-watch:
    runs-on: ubuntu-latest
    if: contains(github.event_name, 'pull_request')
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0

      - run: npx @eqworks/commit-watch -b ${{ github.event.pull_request.base.sha }} -h ${{ github.event.pull_request.head.sha }} -v
```

## On Local Development Branches

Try **NOT** to commit to the main branch directly. Even if you are the sole maintainer now, there is always the possibility of new members joining.

Try to stay up-to-date with the main upstream branch and actively perform `git fetch --prune` to clean up idle references.

Perform controlled commit amends, squashes, and cherry-picks as much as needed to maintain a good commit history (see [`On commits`](#on-commits) section) before pushing to upstream.

Name the branch as `scope/change-title`, or if needed, `scope/sub-scope/change-title` where `scope` depends on a convention on a per-repository basis. Please resist the temptation to bundle out-of-scope commits within each branch. Chain-branch off from the `scope` branch instead of the main branch when functionality requires contiguous commits to work correctly.

```bash
$ git branch
  hub/dataset-flow
* hub/csv/fix-parsing # contiguously branched off from hub/dataset-flow
  main # the main branch of the repo
```

### Common Pitfall - Accidental `git commit` instead of `git rebase --continue`

A [Q&A on Stackoverflow](https://stackoverflow.com/questions/6457044/forgot-git-rebase-continue-and-did-git-commit-how-to-fix) covers this very case. In short:

```bash
# It moves the HEAD pointer to its parent but keeps the work tree
# and adds the merge change to the index
$ git reset --soft HEAD^

# So you can continue rebasing with
$ git rebase --continue  # as before
```

### Common Pitfall - Inclusion of unwanted commits from a rebase
If you included commits you didn't want to, this [Q&A on Stackoverflow](https://stackoverflow.com/questions/134882/undoing-a-git-rebase) would provide a solution. Example:

The easiest way would be to find the head commit of the branch as it was immediately before the rebase started in the reflog:

```
git reflog
```

And to reset the current branch to it (with the usual caveats about being sure before resetting with the `--hard` option).

Suppose the old commit was `HEAD@{5}` in the ref log:

```
git reset --hard HEAD@{5}
```
In Windows, you may need to quote the reference:

```
git reset --hard "HEAD@{5}"
```

You can check the history of the candidate's old head by just doing a `git log HEAD@{5}` (Windows: `git log "HEAD@{5}"`).



### Squash Commits

Squashing commits with `git rebase -i` (`i` for interactive) gives more granular control than `git commit --amend`.

Example:
1. `git rebase -i HEAD~3` brings 3 commits from and including `HEAD`:

```bash
pick 6df9b94 has_aoi - add a query to check if there are associated POIs in the AOI report table
- responses will include a `has_aoi` flag indicating true/false
pick 6d9075c mend
pick 95e9ccd report_vwi - add has_aoi query logic to VWI reports
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
2. edit and replace the keyword `pick` with `squash` (or `s`):

Upon saving, git editor will prompt with the view to edit the commit messages:
```bash
# This is a combination of 2 commits.
# This is the 1st commit message:

has_aoi - add a query to check if there are associated POIs in the AOI report table
- responses will include a `has_aoi` flag indicating true/false

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

This tagging convention would allow for some nice tricks to automate tedious tasks, such as listing out commits between tags and branch HEADs:

```bash
$ git log v1.2.12..HEAD --pretty=oneline --abbrev-commit --author=runzhou.li
c5f91ec Builder/Hub - prevent actions before WL is chosen
7461541 Hub - allow multiple (composite) `primary_key`s
e323208 Hub - deprecate `primary` for `primary_key`
326cc64 Hub - bug fix of ISO date detected as IP, also:
```

From above and combined with good practice [on commits](#on-commits), we can leverage tools like (our own) [`release` CLI](https://github.com/EQWorks/release) to generate nicely arranged release notes or changelog material.

## On Pull/Merge Requests

Try to maintain a good length and depth of the code changes within each request (digestible within 30 minutes or less for the reviewers).

Try to keep a concise summary of changes in the request description. Try to attach screenshots/videos to demonstrate the workflow and before/after differences. Good practices [on commits](#on-commits) help tremendously for summary, so rebase/squash/rephrase commits as needed to keep the commit history clean.

When applicable, reference and mark relevant issues as fixed/closed (e.g., `fixes #123`).

Start the request as a draft or mark in the title with a `[WIP]` prefix when it needs more time to complete. Then, mark it ready to review or with a `[G2M]` prefix in the title to signal its readiness.

When reviewers approve the PR, it's ready for merging. There are three ways to merge it through GitHub:

### Create a merge commit

Merge with [`--no-ff` option](https://git-scm.com/docs/git-merge#_fast_forward_merge) gives a good indicator (the merge commit) of the bundling of code change commits. Also, merging with a merge commit preserves the commit history and its timeline.

![merge commit](https://user-images.githubusercontent.com/2837532/121074564-09531000-c7a2-11eb-8a56-39e238ab4b1c.png)


### Squash and merge

**TRY NOT TO SQUASH MERGE.**

### Rebase and merge

The relevant commits are all rewritten to be on [top of the `HEAD` of the target branch](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=le). The rebase action can alter the commit history and its timeline. In return, you gain a whole block of commits representing intended code changes next to each other.

## On Reviewing

Try to set aside some quality time as a routine to proactively review others' pull/merge requests as thoroughly as your bandwidth allows. If there's no time or no willingness, do not just approve without reviewing; defer it to some other time or other teammates. You may utilize [GitHub's notification with a `review-requested` filter](https://github.com/notifications?query=reason%3Areview-requested) for applicable GitHub-hosted repositories.

Actively self-review and monitor your own pull/merge requests -- be on the lookout for potential conflicts after merging other pull requests.

When giving code change requests, think twice before submitting -- be reasonable and constructive, and be ready to defend your reasons.

If the code change suggestion does not warrant definitive reasoning but still be constructive in your opinion, make it a non-blocking comment.

Where applicable, go through the changes in deploy preview or your local environment to go through the intended workflow, and check for potential issues.

Prioritize on reviewing bug fixes, then the new features. Use `G2M` as a search filter to minimize noise -- provided that the PR prefix is a well-followed convention in the given repository.

## Migrating commits to a new repository
Occasionally, a feature or component will mature to the extent that it should reside in a separate repository. In this case, "splitting up" the existing repository is desired to extract the feature.

It is preferable to retain the relevant commit history rather than copy-pasting code from the parent repository into a new one.

We should perform the "split" in such a way that the new repository contains only the desired files, and its commit history contains only the commits that have affected those files. To achieve so, we have two options:
*  `git filter-branch -f --index-filter` as described in [this pull request](https://github.com/EQWorks/lumen-ui/pull/1) works well if you have a specific list of files and directories you would like to clone.
* `git subtree split -P` as described in [this Stack Overflow answer](https://stackoverflow.com/questions/28357056/partial-git-clone-with-relevant-history) works well if the desired files constitute a single subdirectory, as the `-P` option denotes "prefix."

---
## General References
- [GitHub article on merge methods](https://help.github.com/en/articles/about-merge-methods-on-github)
- [Git documentation on merge](https://git-scm.com/docs/git-merge)
- [Atlassian article on Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [VS Code as Git editor](https://code.visualstudio.com/docs/editor/versioncontrol#_vs-code-as-git-editor)
