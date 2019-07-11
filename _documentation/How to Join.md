---
layout: article
title: How to join this project
excerpt: "How to join this project"
---
## How to join the project

### Communication

Communication is important. We use Spinsights, Basecamp, and
Github. Get free accounts and look for OpenVnmrJ. OpenVnmrJ has a
presence on Trello and Slack but most planning is done in Basecamp.

In case of doubt, open an issue in the issue tracker (on Github), post
your question to the spinsights/trello/slack or contact one of the
project maintainers on Slack.

Especially do so if you plan to work on something big. Nothing is more
frustrating than seeing your hard work go to waste because your commit
is very large and unwieldy.

#### Spinsights

Spinsights is Agilent's NMR and MRI support board, which is [available
here](https://spinsights.chem.agilent.com). Please ask questions and
provide feedback throught Spinsights or Github.

#### Basecamp

Hosted by Eric Paulson at Yale, OpenVnmrJ is using basecamp for
planning and project management.  (Need URL? is this still active?)

#### Github

The repositories, documentation, and bug tracking are hosted on
[GitHub OpenVnmrJ](https://github.com/OpenVnmrJ).

#### Slack

Join Slack for free. Ping us at
[OpenVnmrJ](https://openvnmrj.slack.com/), Basecamp is preferred.

### Core committers

Core committers are those who have push access to the main OpenVnmrJ
repository that produces OpenVnmrJ. To become a core committer, one
needs to sign the contributor license agreement.
 
One is not required to have a proven history of contributions before
being granted commit access, but that doesn’t mean other core
committers will never revert your changes.

The master branch is protected from deletion and force pushes and so
all updates to the master branch must be done by pull requests.

The list of CLA signers is be maintained here: 
[TODO]

### Contributing new plugins/tools/libraries/appdirs

If you develop a plugin/tool/library/appdir, we encourage you to
co-host that with the OpenVnmrJ project so that other people in the
community can participate.  See Hosting Appdirs for more details.

### Making changes to existing appdirs/macros/pulse sequences

If you are interested in just making a small number of changes 
without an intent to stay. It’s the easiest to send in pull requests 
through GitHub. See using pull requests
for more details. If your pull requests are not getting timely 
attention, please ping us via Slack, so that we 
can resolve that.

If you’d like to be involved more seriously, in addition to the pull 
request, we encourage you to consider becoming a committer. Drop us a 
note in Slack, and we’ll set you up with 
commit access. Try to be courteous to existing developers by sending 
them heads-up and coordinating with them, but if they aren’t responding,
don’t let that block your progress. The seniority of the developers are
earned through on-going participation.

### Helping and taking over dormant appdirs/pulse sequences/macros

It is often the case that the original developer moves onto other 
things once the code becomes good enough for them (or if the original 
author changes the job and no longer has incentive to work on the 
technology.) So we encourage new developers or developers of different 
plugin to pitch in on other plugins’ pending pull requests or work on 
issues filed against them.

To that end, we also encourage people to pick up dormant plugins and 
consider them theirs. To do this, drop us a note at the dev list, and 
try to contact the previous maintainer to find out if they are still 
interested in driving the plugin.

Many less active plugins do not really have any obvious owner, and 
they are collaboratively maintained by people making small changes and 
releasing them whenever the need arises.  If in doubt, ask on the dev 
list.

### Making changes to core code

If you are interested in just making small changes without an intent
to stay, the same process applies as macros and pulse sequences,
described above.  However, because core changes affect larger number
of people, we’d be grateful if you’d try to go extra distance on the
notes described in using pull requests.

If you’d like to be involved more seriously, consider getting commit
access. See the section about becoming a plugin developer for how to
get this. In addition, we need to ask you to sign the contributor
license agreement (CLA).

When making changes, use your common sense. For example, if you are 
thinking about making a big change, it is recommended that you discuss 
your changes with the developers upfront. Or if you see that the part 
you’d like to work on has been actively modified by others, give them a 
heads-up.  

### Contributing localizations

We are always looking for people who can help localize OpenVnmrJ to
different languages. If you are interested in helping, drop us a note
in Slack to get commit access, and see Internationalization for the
details of how to make changes.

## Contributing

See [Contributing](/Contributing) for nitty-gritty details on how to
submit to the core of OpenVnmrJ. See below for some guidance.

### Rebase before merging

The merge commits should make good sense to the history of the
project. Do not commit branches that are full of git commits. Please
rebase and commit a clean branch.

### Cherry picking

Cherry pick across a branch to add need functionality quickly. 

### Code review

At least two people should read through each commit. Large commits are
difficult and take a long time to code review, so commit smaller
chunks.  Let core committers know if a large commit is coming, and let
them know well in advance, perhaps before you start!

### Using pull requests

As discussed above, OpenVnmrJ project uses pull requests as one of the 
main workflow to get the changes in. When you prepare your pull request,
consider the following checklist as the best practice.

* See the github online help for how to create a pull request  
* Basically, fork one of the repositories into your github account. Then clone the repository to your local computer.  
Add the fork as an upstream repository so you can push changes to your fork. 
Now, create a branch so you can identify your changes. 
Name the branch usefully, for example, if you are fixing ISSUE-123, name it “fix-issue-123”. 
Branch from development or a feature branch, don’t branch from the stable branch unless you are back porting an important fix.  
* Always write tests for you changes. Commit when you are done. Push your changes. 
Go to github and file a pull request.
* Before you start, please file a ticket in the issue tracker to describe the bug that 
you are fixing or the feature you are implementing. This creates a permanent record on our system that allows 
future developers to understand how the code came into the current shape. 
This is not a requirement (especially for small changes), but we appreciate if you do that.  
* Refer to the ticket in your commit message by using the notation [OpenVnmrJ-1234] where OpenVnmrJ-1234 is the ticket ID. 
This allows our scripts to understand the history and generate change logs without human help. If you use the notation [FIXED OpenVnmrJ-1234], 
our bot will close the ticket automatically when the change is merged into the repository, 
and when the change is tested in our CI server. These notations create useful cross-references across systems, 
and are therefore highly recommended. We encourage you to have a test case for the code you added to avoid future regressions.  
* See Unit Test for more details about how to write tests. Try to describe your changes 
so that other people understand what you did. Make sure you didn’t modify portions that aren’t related to your changes 
(most often caused by IDE auto-fixing import statements and other code formats.)
* If you notice that your pull requests aren’t getting attended to within a week or two,
 please drop us a note in Slack, and please consider becoming a committer and push the changes directly. 
 See Pull Request to Repositories for more.  

### Copying Code from elsewhere

When you have a license to do so, and when that license is compatible with the Apache 2.0 license, you can copy the code from elsewhere into OpenVnmrJ.

The most typical case of this is that the original code is licensed under a certain subset of the open-source licenses, 
such as ASL, BSD, and MIT license.   
Copyleft licenses, even though they are open-sourced, __cannot be copied__, such as EPL and GPL, *unless it is part of the GPL components of OpenVnmrJ*. 

The code to be copied must be clearly marked with the license it is under, and when copying, you need to maintain the copyright/license attribution in the header. 
Please also indicate the origin of the copy as a part of the commit message.

### Code of Conduct

We expect all contributors to follow the [Code of Conduct](/Code of Conduct). This code of conduct outlines our expectations for participants within the OpenVnmrJ community, as well as steps to reporting unacceptable behavior. We are committed to providing a welcoming and inspiring community for all and expect our code of conduct to be honored. Anyone who violates this code of conduct may be banned from the community.
