# Git Katas

## Notes:

You should never use `push --force` or equivalent unless otherwise stated

You should try and perform all the tasks listed here using the command line first,
and relying on a tool like `sourcetree` after.

## Task 1 - Create a new empy repo

```bash
$ cd
$ mkdir repos
$ cd repos
$ mkdir kata
$ cd kata
$ git init
$ # create a file named 'hello.txt' containing "Hello, worldd"
$ git add hello.txt
$ git commit -m "Initial commit"
```

It's possible git will ask you to configure your name and email before
allowing you to commit - if so, do what it says.

Then verify using `git log` that you did create a commit

## Task 2 - Clone this repo

The first task is to clone this repo in a place where you have *write* access.

You can either fork it on GitHub, or re-create it from scratch on GitLab for instance.

## Task 3 - Simple commit

* Edit a file in this repo
* Make a change
* Make sure the changed are saved
* Add the file with `git add <file>`
* Make a commit with `git commit -m "<message>"`

## Task 4 - git log, git blame

There's a typo in the file `numbers.txt` - find the name and email of the
dev who is responsible for this !

## Task 5 - The cycle of collaboration

*Goal: learn how to share a branch across the same team*

Make sure Alice and Bob both have cloned the repo

* Alice: add your name to the THANKS
* Alice: make a commit with the message "Add Alice to THANKS file"
* Alice: push the commit to the main branch
* Bob: get Alice's changes from the main branch (using `fetch` and `merge` for instance)
* Bob: make a commit with the message "Add Bob to THANKS file"
* Bob: push the commit to the main branch
* Alice: update the main branch

Alice should end up with a log looking like this:

```diff
* 6430036 - Add Bob to THANKS file (62 seconds ago) <bob>
--- a/THANKS
+++ b/THANKS
@@ -1 +1,2 @@
 Alice
+Bob

* a6c829f - Add Alice to THANKS file (2 minutes ago) <alice>
-
+Alice
```

## Task 6 - Two commits from one file

*Goal: learn about the git index*

This should be done by each member of the team.

* Change at least two different lines in `index.html` file (I'm sure you can find something to improve)

* Make two commits, each one containing a different line change.

## Task 7 - Undoing changes

*Goal: learn about the various ways to undo changes in git*

This should be done by each member of the team.

* Revert the two commits made during task 2

* Change a few lines in `index.html` and then restore the file to its original version

* Move the head of the branch to where it was before task 2 started branch

## Task 8 - Happy merge

*Goal: show how to merge in the trivial case*

* Alice: Change the `<title>` in `index.html`
* Alice: push the changes to the main branch
* Bob: do *not* fetch Alice's changes
* Bob: change something in the JavaScript code
* Bob: make a commit and try to push it to the main branch - git will ask
  your to merge first
* Bob: merge your branch and push the result

## Task 9 - Happy  rebase

Some as the previous one, but use `rebase` so that there is no merge commit in the history.

## Task 10 - Conflict resolution

*Goal: learn about merging conflicting changes*

* Alice: Edit 'conflict.txt' and add the following text on line 2:

> C'est la goutte d'eau qui met le feu aux poudres

* Alice: make a commit and push it to the main branch

* Bob: make sure to *not* fetch Alice's changes at this point.

* Bob: Edit 'conflict.txt' and add the following line also on line 2:

> C'est l'étincelle qui fait déborder le vase

* Bob: make a commit and try to push it to the main branch - git will ask
  your to merge first

* Bob: try and merge - git will tell you that there are conflicts

* Alice & Bob: resolve the conflict and push the resolution

## Task 11 - Cherry-picking

If you look at the repo, you will see that the 'release' branch does not contain
the commit that bumps the year in the `COPYRIGHT` file (which is expected since it was
created in 2021).

Use `git diff` to confirm this.

Then use cherry-picking to fix the COPYRIGHT year on the `release` branch as well

Finally, create an push a `v1.1` tag on the release branch

## Task 12 - Interactive rebase

Switch to the `dev` branch.

Verify that there are 5 commits between `main` and `dev` (most recent last):

```
* Add transaction parser
* Refactor old code
* Compute transaction price
* Fix issue on parser
* Compute transaction price: add test
```

Use an interactive rebase of `dev` on top of `main` so that the history
looks like this:

```
* Refactor old code
* Add transaction parser
* Compute transaction price
```

Hints:

* You can do it in several passes
* You can create a tag to verify your rebase does presevre all the changes

## Task 13 - Code review

* Alice: Add some code in 'index.html'
* Alice: Make sure to include a small mistake in the code you added
* Alice: Make a commit and push it in a branch named 'fix-style'
* Alice: Create a merge request (GitLab) or a pull request (GitHub)
* Bob: look at Alice's changes and leave some comments about the typo
* Alice: Use rebase or `git commit --amend` to address Bob's feedback and fix
  the typo (you are allowed to use `push --force` this time)
* Bob: Merge Alice's branch

