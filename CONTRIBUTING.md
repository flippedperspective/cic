Contributing Guidelines
=======================

CIC does its best to maintain a clean and useful commit graph. To help achieve that goal, it follows some fairly strict guidelines for how Pull Requests look.

To simplify the language in these explanations, we will use the following definitions in this document with respect to Pull Requests:

* source branch: The source branch is the branch containing the newly developed code that needs to be pulled
* target branch: The target branch is the branch into which the source branch should be merged

Commit messages should be appropriately styled
-------------------------------------------------------------------

Commit messages should be a short description of what the commit is doing. If necessary, they can contain a longer explanation after the description. The explanation should be separated from the description by a blank line. Any meta content used for automated processes should appear before the explanation and also be set off by a blank line.

Descriptions should be grammatically correct and use the imperative instead of past- or present-tense. That is, prefer "Fix" to "Fixed" or "Fixes". Descriptions should not end in a period.

Descriptions should also not be longer than 64 characters. Keeping descriptions short is helpful since many tools, such as GitHub's display, `git shortlog`, and `git rebase -i` use the description. Long commit messages will be truncated in many cases, and the truncation may make the message useless. The 64 character limit was arrived at as the maximum number of characters that will display nicely in most editors during a `git rebase -i`.

Where descriptions should always explain the what of a commit, explanations can contain the why. They may also contain more in depth explanations of what. In most cases, anything in the explanation portion of a commit message should also be documented somewhere in the commit itself: either in a comment in code or in a documentation file.

The explanation should be wrapped at 72 characters so it will display nicely in terminals. If styling is needed in the explanation, such as lists or tables, attempt to use Markdown if possible. GitHub Flavored Markdown is acceptable, though explanations

The basic rationale behind most of these decisions is well explained by [Tim Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).

Rebase the source branch branch instead of merging into it
---------------------------------------------

CIC likes to have feature developments consist of one fork and one merge. Features that take a while to develop may have conflicts that prevent them from being merged back into the target branch. It is tempting to use `git merge` to resolve those conflicts, but this violates the one fork and one merge philosophy. Instead, use `git rebase` to rebase the source branch onto the target branch.

While this may seem like an extra burden, especially since some changes may merge more cleanly than they rebase, it tends to not be much more work when taken in the context of the rest of the guidelines.

Squash commits that don't provide meaningful changes
----------------------------------------------------

CIC prefers to keep the number of commits in a Pull Request small and to minimize the number of commits in the whole log. This makes it much easier to understand the changes in the Pull Request, or to find specific changes in the log.

When developing and committing frequently, invariably there will be some commits in the graph that don't add meaningful changes. These include commits that add or remove temporary debugging logic, commits that fix typos or syntax errors, and other mostly trivial changes.

CIC prefers to have these small commits squashed before accepting a Pull Request. There are a couple techniques we use to help squash these commits.

* Use `git rebase -i` before submitting a Pull Request to manually remove any small commits that may have been added.
* When submitting a fix to the last commit made, such as adding a missing semi-colon, use `git commit --amend -C HEAD`. This immediately squashes the new commit onto `HEAD` without touching the commit message.
* When fixing an older commit, use `git rebase -i` to reorder the commits and make the older commit `HEAD`. Then use `git commit --amend -C HEAD` to fix the commit. Optionally use `git rebase -i` to put the commit back where it was in the history.

Since rebasing is used fairly frequently to fix commits, it is typically done after a `git fetch origin`. That way, when the target branch is specified as the new branch, any changes that may cause conflicts can be resolved, and the temptation to later perform a merge is reduced.

Pull Request Checklist
======================

- [ ] Rebase the source branch onto the target branch
- [ ] Squash any commits that don't add meaningful changes
- [ ] Commit messages contain no typos
- [ ] Commit messages use the imperative and do not end in a period
- [ ] Commit messages consist of a description followed by an optional longer explanation separated by a blank line
- [ ] Commit message descriptions are 64 or fewer characters
- [ ] Commit message descriptions use the imperative
- [ ] Commit message descriptions do not end in a period
- [ ] Commit message explanations are wrapped at 72 characters
- [ ] Commit message explanations use Markdown for styling
- [ ] Commit message meta-content for automation is before the explanation and offset by blank lines