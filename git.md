# git

## On Commits

GOOD:
- Concise and relevant commit messages.
- Each commit as isolated from each other as possible.

BAD:
- Commit messages that contribute no value to the readers of your code -- such as `test`, `lint`, `debug`, `adsfasdf`.
- Commit changes not properly reflected in commit message -- use `$git commit --amend` to fix the message.

## On Branches

GOOD:
- Always stay up-to-date with the upstream main branch (usually `master`) through `rebase` or `merge`. Follow [this rule](https://www.atlassian.com/git/tutorials/merging-vs-rebasing#the-golden-rule-of-rebasing) when deciding on whether to `rebase` the main branch into your working branch.
- Perform controlled squashes as much as needed, to maintain a good commit history (see [`commit`](#commit) section above).
- Bundle and cherry-pick only relevant commits, within a designated scope.
- Name the branch as `scope/change-title`, and if absolutely necessary, sub-scoped as `scope/sub-scope/change-title`.

BAD:
- Leave local and remote diverged -- force-push in a working branch is ok.
- No irrelevant commits to the designated scope -- start branch(es) to apply those.
- Too many sub-scopes -- preferably only one `/` in the branch name.

## On Pull/Merge Requests

GOOD:
- Control the length and depth of the code changes within each request, make it digestible within 30 minutes, or even less.
- Write [`CHANGELOG`](https://keepachangelog.com)-like summaries of changes in the request description. Try to attach screenshots/videos to demonstrate the workflow and before/after differences.
- Do either merge commit or rebase merge:
    - Through **merge commit** (merge with [`--no-ff` option](https://git-scm.com/docs/git-merge#_fast_forward_merge)) -- this gives a good indicator (the merge commit) of the bundling of code change commits. Also, the commit history and its timeline are [fully preserved](https://wac-cdn.atlassian.com/dam/jcr:e229fef6-2c2f-4a4f-b270-e1e1baa94055/02.svg?cdnVersion=le).
    - Through **rebase merge** -- the relevant commits are all rewritten to be brought on [top of the `HEAD` of the target branch](https://wac-cdn.atlassian.com/dam/jcr:5b153a22-38be-40d0-aec8-5f2fffc771e5/03.svg?cdnVersion=le). That means the commit history and its timeline _can be_ altered. In return, you gain a full block of commits that represent intended code changes next to each other.
- Either mark the issue(s) that the request fixes (`fixes #123`, `closes #321`), or label the request itself when there are no relevant issues -- not both.

BAD:
- Lengthy code changes -- this often requires some forward thinking on how to structure the changes (TODO: to be discussed in another section).
- No description -- unless the title alone suffices all the changes.
- Label requests that already have target issue(es).
- Squash merge into the main branch -- this reverts our previous practice, read above and understand why.

## On Reviewing

GOOD:
- Set aside some quality time as a routine to proactively review others' pull/merge requests, as thoroughly as your bandwidth allows.
- Actively self-review and monitor your own pull/merge requests -- be on the lookout for potential conflicts after other requests have been merged.
- When giving code change requests, think twice before you submit -- be constructive, and be ready to defend your reasons.
- If the code change suggestion does not warrant definitive reasoning, but would still be constructive in your opinion, make it as a non-blocking comment.

BAD:
- Cast approval without actually reviewing it -- this is obvious, as code reviews should be for quality control, **not** for bureaucratic control.
- Speak with a bad tone, or demand *your* own opinion as a code change request -- read what you wrote, phrase or code, as if it was given to you, see if it justifies.

## General references

- [GitHub article on merge methods](https://help.github.com/en/articles/about-merge-methods-on-github)
- [Git documentation on merge](https://git-scm.com/docs/git-merge)
- [Atlassian article on Merging vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
- [VS Code as Git editor](https://code.visualstudio.com/docs/editor/versioncontrol#_vs-code-as-git-editor)
