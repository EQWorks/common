# Common

Common practices and disciplines that help to minimize common obstacles and frictions for a good work culture and environment.

## git

### Commits

GOOD:
- Concise and relevant commit messages.
- Each commit as isolated from each other as possible.

BAD:
- Commit messages that contribute no value to the readers of your code -- such as `test`, `lint`, `debug`, `adsfasdf`.
- Commit changes not properly reflected in commit message -- use `$git commit --amend` to fix the message.

### Branches

GOOD:
- Always stay up-to-date with upstream main branch (usually `master`) through `rebase` (or `merge` with `rebase` strategy).
- Perform controlled squashes as much as needed, to maintain a good commit history (see [`commit`](#commit) section above).
- Bundle and cherry-pick only relevant commits, within a designated scope.
- Name the branch as `scope/change-title`, and if absolutely necessary, sub-scoped as `scope/sub-scope/change-title`.

BAD:
- Leave local and remote diverged -- force-push in working branch is ok.
- No irrelevant commits to the designated scope -- start branch(es) to apply those.
- Too many sub-scopes -- preferrably only one `/` in branch name.

### Pull/Merge Requests

GOOD:
- Control the length and depth of the code changes within each request, make it digestable within 30 minutes, or even less.
- Write [`CHANGELOG`](https://keepachangelog.com)-like summaries of changes in request description. Try to attach screenshots/videos to demonstrate workflow and before/after differences.
- Always do either merge through merge commit (merge with [`--no-ff` option](https://git-scm.com/docs/git-merge#_fast_forward_merge)) or rebase merge. Each has its own merits, _so we leave this open for now_.
- Either mark the issue(s) that the request fixes (`fixes #123`, `closes #321`), or label the request itself when there are no relevant issues -- not both.

BAD:
- Lengthy code changes.
- No description -- unless the title alone suffices all the changes.
- Label requests that have target issue(es).
- Squash merge into main branch.
