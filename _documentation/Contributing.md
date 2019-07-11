---
layout: article
title: Contributing
excerpt: "Instructions on how to contribute to the OpenVnmrJ project."
---
{% include toc.html %}

## Our Philosophy

### Low barrier of entry

We strive for a low barrier of entry to the project. This is partly
achieved by not requiring new contributors to “prove themselves”
before they are admitted to the "committership" (or some other
honorific).  Instead, we assume that all contributors are good until
proven otherwise, and this principle applies to anybody without
arbitrary discrimination. We recognize that every contribution is
precious, and we recognize that every added process turns away some
potential contributors.

The lower barrier of entry is partly achieved by separating the
project into "core", "appdirs" (groups of pulse programs, macros, &
templates), documentation, and other independent pieces, thereby
reducing the need for extended collaboration and communication. We try
to let everyone choose their own turf where they can work efficiently
without bogged down by too many discussions and compromises.

The lower barrier of entry is also partly achieved by recognizing that
people move on. Lots of code in the project is maintained by people
other than the original author. We encourage new contributors to take
over existing parts that aren’t actively maintained. We believe that
“old” contributors deserve respect from “new” contributors, but the
inaction on the part of the original contributors shall not block new
contributors from making changes.

Even users unfamiliar with code can contribute: install and run the
development versions of OVJ, file bugs on github, let the developers
know what features/fixes are important to you, suggest improvements,
and join discussions

### Meritocracy

Our striving to a low barrier of entry doesn’t mean everyone has the
equal voice. We value those who contribute more to the project, namely
Meritocracy. Contribution shouldn’t be narrowly interpreted just as
code changes, but rather it includes such activities as helping others
in the OpenVnmrJ community, producing documentation, running
infrastructure, and so on.

### Code of Conduct

We expect all contributors to follow the [Code of Conduct](/Code of Conduct). This code of conduct outlines our expectations for participants within the OpenVnmrJ community, as well as steps to reporting unacceptable behavior. We are committed to providing a welcoming and inspiring community for all and expect our code of conduct to be honored. Anyone who violates this code of conduct may be banned from the community.

### Transparency

We believe in running the project transparently. This includes everything from decision-making to defects in the code.

### Compatibility matters

We recognize that users expect their existing data, accumulated under past versions (including commercial versions) to continue working under future versions of OpenVnmrJ. This includes pulse sequences, macros, and spectrometer configurations that they are using. The OpenVnmrJ project places high value on maintaining this compatibility, and will be very careful in removing functionality.

The use of modules, called applications directories (or "appdirs"), is strongly encouraged (if not mandatory) for adding any functionality that is large in scope. Also in this spirit, minimizing any needed changes to the "core" code for new features is strongly preferred.

## How to join this project

See the document [How to Join](/How to Join) for more details.  

## Technical details

The github repository is https://github.com/OpenVnmrJ/ and only a
documentation page exists at this time. Sign up for a free github
account to access the repository. With github all changes are made
offline and merged back in.

You’ll need to have git (a set of command line programs) installed on your computer and/or a git UI (if you are uncomfortable with the command line), see:

- https://windows.github.com
- https://mac.github.com
- http://gitup.co/
- http://gitx.frim.nl

On Ubuntu: `sudo apt-get install gitk`

On RedHat: `yum install git`

### Branch information

* If we have a cycle of regular development, we may have version branches.
* Keep your commits small and atomic, for example adding a function or fixing a bug, but not both at once.  
* Commits must not touch many files at once, with the exception of trivial changes, such as copyright. Try to break your commit into small, more contained changes.  
* Flatten your commit before you make a pull request.  
* Rebase from the latest development branch  

### Appdirs

OVJ uses Appdirs; modular code that resides in "Application
Directories" and can be optionally loaded at run-time to reconfigure
the UI, pulse sequences, macros, etc. If a new feature can be
implemented via a Appdir without changes to the Core OVJ code, this is
greatly preferable.

If you have minor features to add or changes to existing macros,
templates, or pulse sequences, please put this work in the "develop"
Appdir ("openvnmrj-develop"). When a new release of OVJ is made, the
"develop" Appdir will be merged into a release Appdir.

If you have a significantly new feature or a very large number of
files and changes, you should make your own new, separate Appdir (with
its own name) in the Development branch of the OVJ code.

### Important tips

* Always work from a feature branch. Since all code submissions will
  be through a Pull Request, feature branches isolate changes from one
  submission to another.
* Always start your new branch from the development branch: `git
  checkout -b myfeature development`
* Remember to submit your Pull Request to the development branch and
  not master

### Git workflow

We will have a UI for OpenVnmrJ such that users will be able to install and submit 
contributions as appdirs to OpenVnmrJ. This is technical and for users who want more
control over their submissions or are interested in changing the core of OpenVnmrJ.

_This is a public repository._

A "quick" summary of how to use change/add files is:

1. Fork this repository into your own account (Use github UI, see https://help.github.com/articles/fork-a-repo/)
2. Download the forked repository to your computer (Use github UI or `git clone repo-url`)
3. Checkout the development branch: 
```
git checkout development
git pull
```
4. Start your branch `git checkout -b "my feature"` (see branches below)
  1. Always start a new branch for your work, so it can be merged in later,   
  2. Branch from master
5. Make your changes, add, delete files on your own computer
  1. Do not all files local to your computer (that are not needed to be shared) to the repository
6. Rebase frequently to pull in changes from the upstream
`git rebase upstream master`
6. Commit your changes
  a. Use the `git commit --fixup` to easily squash later
7. After you have finished the feature, if you have many commits squash them, see below
  1. See https://robots.thoughtbot.com/autosquashing-git-commits for to easily squash commits
  2. It is important to clean up commits before they are shared!
  3. Write a good commit; you shouldn't have many commits, since you've squashed them. See http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
```
Present-tense summary under 50 characters

* More information about commit (under 72 characters)

[PROJECT TICKET]
```
8. Push your changes back to your fork
  a. You might need to force your push if you've squashed commits
9. Make a pull request back to the OpenVnmrJ/master branch, see Git Pulls, below

 A bit complicated for one page, but it works well with hundreds of files and hundreds of contributors.
 
See https://sandofsky.com/blog/git-workflow.html for a background on git workflow.

### Branches

`git checkout -b "my feature"`  
See https://www.atlassian.com/git/tutorials/using-branches/git-checkout on how to make a branch and use branches  

### Git pulls

See https://help.github.com/articles/using-pull-requests/  
“Fork and pull” model is good for this project (when there are more contributors).  
The GitHub UI can be used. Review the changes and  
`git merge --no-ff development`

### Delete your feature branch

Delete your feature branch once done with it, on your fork on github:

`git push origin --delete <branch-name>`
In your local repository  
`git branch --delete <branch-name>`

## The future

We will work on making this transparent to users in the following cases:  
1. Submitting pulse sequences
2. Submitting macros

### VnmrJ macros and Appdirs

To make this process easier, we will divide the source into repositories and use VnmrJ macros. This is a work in progress.

