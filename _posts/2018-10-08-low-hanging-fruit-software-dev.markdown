---
layout: post
title:  "Low-hanging Fruit in Software Development Process for CS Research Projects"
date:   2018-10-08 12:00:00 -0500
categories: Meetings
published:  false
---

For more, check https://guides.github.com/introduction/git-handbook/

## Goal of Revision Control

**Traceability**

+ Which changes were made?
  (What stupid thing did I do?)
+ Who made the changes?
  (Which version of me did this stupid thing?)
+ When were the changes made?
  (When was I so stupid?)
+ Why were changes needed?
  (What were the stupid reasons that make me did the stupid thing?)

+ **NOT** a remote backup of everything on you computer

## Basic Git commands

+ `git clone` creates a local copy of a project that already exists remotely
+ `git add` stages a change
+ `git commit` saves the snapshot to the project history
+ `git status` shows the status of changes as untracked, modified, or staged
+ `git branch` shows the branches being worked on locally
+ `git merge` merges lines of development together
+ `git pull` updates the local repository with updates from remote repository
+ `git push` updates the remote repository with commits made locally

## More helpful Git commands

+ Staged Changes (after `add` before `commit`)

    - `git diff` and `git diff --cached`
    - `git reset HEAD`

+ Local Repository (after `commit` before `push`)

    - `git commit --amend`, modify/update `HEAD` commit
    - `git reset <commit>`, discard all commit history after `<commit>`
    - `git revert <commit>`, make a new commit that undo the changes made at `<commit>`

        + Using this instead of manually changing it back allows git to discover
          automatic merge strategy more easily

    - `git rebase -i`, reduce unnecessary merge commits by rebasing the local branch

+ Remote Repository (where you `push` to and `pull` from)

    - `git remote show <remote-name>`
    - You really can't/shouldn't change the history on the remote repository


## Git Practice

Tool-assisted

+ Unify line endings with `.gitattributes`
+ Avoid committing unnecessary files with `.gitignore`
+ Enforce code review via protected `master` branch and pull requests

Personal Discipline

+ Meaningful commit messages
+ Small changes everyday or every hour is much better than a huge chunk of changes of a week

    - Even when you finished a chunk in a day, try to divide into small parts
      and commit separately
    - Leave *TODO* as placeholders and finish work in later commits

## Continuous Integration

+ Automatic Style Checking, Building, and Testing
+ 


## Coding Practice

+ Unit tests