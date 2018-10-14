Curation with Git
=================
This document describes a workflow for doing BEL curation using git for
version control. It's inspired by the `Git Flow <https://danielkummer.github.io/git-flow-cheatsheet>`_
philosophy.

The purpose of this document is not to explain what git is or how to use it.
Lots of fantastic resources exist on the internet for this - here's a good
place to start: https://guides.github.com/activities/hello-world/.

1. Make a Branch
----------------
The main/master branch of the git repository is protected in order to encourage assessment
by multiple users.

1. Check out the master branch
2. Fetch and pull from the origin
3. Make a new branch with a descriptive (but succinct) name of what you'll be working on.
   If this branch corresponds to adding a new article, title the branch with the author's
   last name and publication year prefixed with ``curation-``. Example:
   ``curation-olsen2016``

2. Commits with Incremental Progress
------------------------------------
Commit early and often. Each commit should describe what's being worked on, and follow
best community practices for writing the commit. See: https://chris.beams.io/posts/git-commit/.
In the future, pre-commit hooks could be used to enforce this policy.

Between commits, locally compiling the BEL document with a compiler like `PyBEL <https://github.com/pybel/pybel>`_
to find errors is helpful as opposed to waiting until the whole curation task is finished. Other solutions using
continuous integration to take the hassle out of installing and running a BEL compiler are also publicly available.
For example, see: https://github.com/cthoyt/pybel-git.

3. Merge
--------
If curation is being done on GitHub, make a `pull request
<https://help.github.com/articles/creating-a-pull-request/>`_. On GitLab, make a `merge request
<https://docs.gitlab.com/ee/gitlab-basics/add-merge-request.html>`_. This is a place where the
final results can be checked one more time for syntactic/semantic correctness with PyBEL, and
discussion between curators and managers can occur.

Each merge/pull request needs a name suitable for the public commit log, since the multiple
commits will be combine (through a process known as squashing) before merging onto the master
branch.
