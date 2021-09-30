---
layout: post
title:  "Software Development Practices for CS Research Projects"
date:   2018-10-08 12:00:00 -0500
categories: Notes
published:  true
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

        + You really can't/shouldn't change the history on the remote repository
    
    - `git remote set-url <remote-name> <new-url>`

        + Changing a remote repository's URL. Useful when changing from https to ssh protocol
          or migrating repositories from GitHub to school private Git host for example.


## Git Practice

Tool-assisted

+ Unify line endings with `.gitattributes`
+ Avoid committing unnecessary files with `.gitignore`
+ Enforce code review via protected `master` branch and pull requests

Personal Discipline

+ Take an extra minute to leave a meaningful commit message.
+ Small changes everyday or every hour is much better than a huge chunk of changes of a week

    - Divide large number of changes into small chuck of incremental changes.
      It will be easier to understand the rationale behind the commits.
      A rule of thumb is try to change less than five files at a time.
    - Leave *TODO* as placeholders and finish work in later commits


## Testing

+ Each unit test file should be self-contained.
  Avoid reading files as much as possible bacuase reading files easily causes flaky tests.
+ For developing Python packages, tests should be outside of the package because of following reasons:

    - The tests should be able to run outside of the package to mimic how users use the package.
      This can quickly detect if your code assumes some strict folder structures that causes troubles
      for importing packages.
    - Users of the package should not need to download the test files.
      If they need to download test files to use the package,
      there are code in your tests that should be in your package instead.
    - Test code may depend on more Python packages than needed by users.
      For examaple, Matplotlib is often used to visualize the result; hence sometimes we use it to
      visually check the correctness of test results.
      However, Matplotlib is often unnecessary in order to use some methods in a package,
      but installing Matplotlib normally requires a bunch of other dependecies.


## Continuous Integration

+ Automatically rerun Style Checking, Building, and Testing every time a new commit is pushed
