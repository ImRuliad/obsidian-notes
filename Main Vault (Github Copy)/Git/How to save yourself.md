*You will mess up. Heres how to recover.*

## Scenario: You're working on a feature, your boss asks you to fix a bug *right now*. You aren't ready to commit.
```bash
git stash
```
- ***What to do:*** takes your uncommitted changes and puts them in a temporary storage drawer. You can switch branches, fix the bug, come back, and run ***git stash pop*** to bring your changes back.

## Scenario: You just committed, but forgot to add one file, or made a typo in the commit message.
```bash
git commit --amend
```
- ***What to do:*** Stage the forgotten file, run this command, and it updates the ***previous*** commit instead of creating a new one.

## The "Undo" Button
```bash
git reset --soft HEAD~1
```
- ***What it does:*** Undoes the last commit but keeps the files in your staging area (SAFE)
```bash
git reset --hard HEAD~1
```
- ***What it does:*** Undoes the last commit and DELETES the changes from your files. (DANGEROUS)

## Scenario: A bug was introduced 3 weeks ago and merged into main. You can't rewrite history because others have pulled that code.
```bash
git revert <commit-hash>
```
- ***What to do:*** running this command creates a new commit that records the reverting changes of the previous commit(s). Safe, polite way to undo changes in public branches.
