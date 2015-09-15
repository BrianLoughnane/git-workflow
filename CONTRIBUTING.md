# Contributing

## General Workflow

1. Fork the repo
1. Cut a namespaced feature branch from sprint
1. Make commits to your feature branch. Prefix each commit like so:
  - (feat) Added a new feature
  - (fix) Fixed inconsistent tests [Fixes #0]
  - (refactor) ...
  - (cleanup) ...
  - (test) ...
  - (doc) ...
1. When you've finished with your fix or feature, Rebase origin changes into your branch, then submit a merge request to sprint. Include a description of your changes.
1. Your pull request will be reviewed by another maintainer. The point of code
   reviews is to help keep the codebase clean and of high quality and, equally
   as important, to help you grow as a programmer. If your code reviewer
   requests you make a change you don't understand, ask them why.
1. Fix any issues raised by your code reviewer, and submit a new merge request with a single new commit.
1. Once the code has been successfully reviewed and tested, you will be notified via JIRA.  At this point you can merge your branch into the sprint branch, then delete the source branch.

## Detailed Workflow

### Clone the repo

Use GitLab’s interface to make a clone of the repo.  It will be set to the remote name "origin".

### Cut a namespaced feature branch from sprint

``` bash

# Creates your branch and brings you there
git checkout -b `your-branch-name`
```

Your branch should follow this naming convention:
  - JIRA_ID-some-descriptive-adjectives

### Make commits to your feature branch. 

Prefix each commit like so
  - (feature) Added a new feature
  - (bugfix) Fixed inconsistent tests [Fixes #0]
  - (refactor) ...
  - (cleanup) ...
  - (test) ...
  - (docs) ...

Make changes and commits on your branch, and make sure that you
only make changes that are relevant to this branch. If you find
yourself making unrelated changes, make a new branch for those
changes.

#### Commit Message Guidelines

- Commit messages should be written in the present tense; e.g. "Fix continuous
  integration script".
- The first line of your commit message should be a brief summary of what the
  commit changes. Aim for about 70 characters max. Remember: This is a summary,
  not a detailed description of everything that changed.
- If you want to explain the commit in more depth, following the first line should
  be a blank line and then a more detailed description of the commit. This can be
  as detailed as you want, so dig into details here and keep the first line short.

### Rebase origin changes into your branch

Once you are done making changes, you can begin the process of getting
your code merged into the main repo. Step 1 is to rebase origin
changes to the sprint branch into your cut branch by running this command
from your branch:

```bash
git pull --rebase origin sprint
```

This will start the rebase process. You must commit all of your changes
before doing this. If there are no conflicts, this should just roll all
of your changes back on top of the changes from origin, leading to a
nice, clean, linear commit history.

If there are conflicting changes, git will pause rebasing to allow you to sort
out the conflicts. You do this the same way you solve merge conflicts,
by checking all of the files git says have been changed in both histories
and picking the versions you want. Be aware that these changes will show
up in your pull request, so try and incorporate origin changes as much
as possible.

You pick a file by `git add`ing it - you do not make commits during a
rebase.

Once you are done fixing conflicts for a specific commit, run:

```bash
git rebase --continue
```

This will continue the rebasing process. Once you are done fixing all
conflicts you should run any existing/new tests to make sure that everything works properly.

If rebasing broke anything, fix it, then repeat the above process until
you get here again and nothing is broken and all the tests pass.

### Push your changes to your remote branch

```bash
git push origin your-branch-name
```

### Make a pull request

Make a clear pull request from your branch to the origin sprint
branch, detailing exactly what changes you made and what feature this
should add. The clearer your pull request is the faster you can get
your changes incorporated into this repo.

At least one other person MUST give your changes a code review, and once
they are satisfied they will move your code into the QA phase. Alternatively,
they may have some requested changes. You should make more commits to your
branch to fix these, then follow this process again from rebasing onwards.

Once you get back here, resubmit your code for further review and
someone will look at your code again. If they like it, it will get moved to QA testing,
otherwise, just repeat again.

Once your code has passed the QA tests, it will be ready for merge.  At this point, you can merge your feature branch into sprint, and delete your feature branch.

**Pull requests should be small and occur often.**  Strive to fix one small thing in each pull request.

Your pull request should be comprised of a squashed commit if there are several commits that are working to the same end.  For example, the following commits:

78a3993 2015-06-24 | (doc) add readme introduction (origin/doc) [BrianLoughnane]
0759486 2015-06-24 | (doc) add readme body (origin/doc) [BrianLoughnane]
0d393d6 2015-06-24 | (doc) add readme conclusion (origin/doc) [BrianLoughnane]

can be squashed into one commit:

5d3a3e6 2015-06-24 | (doc) add readme information (origin/doc) [BrianLoughnane]

## Squashing Commits

1. Soft reset to the commit occuring before the commits you would like to squash:
  ```bash
  git reset --soft [prior commit hash]
  ```
1. Commit changes.  Include a message that explains all commits being squashed.


### Bringing in changes from other local branches, if any

If you need to merge two local branches for some reason, use the following workflow:

Say you are merging local branch bugfix into local branch feature

From local branch feature...

1. git pull --rebase origin sprint
1. git checkout bugfix
1. git rebase feature
1. git checkout feature
1. git merge --ff-only bugfix 

Now your feature branch will have incorporated the bugfix branch.  From here you can run your tests, push 
to your remote repo's "feature" branch, then submit a pull request to the main repo's sprint branch.

### Guidelines

1. Uphold the current code standard:
    - Keep your code [DRY][].
    - Leave code cleaner than you found it.
    - Follow [STYLE-GUIDE.md](STYLE-GUIDE.md)
1. Run tests the before submitting a pull request.
1. Submit tests if your pull request contains new, testable behavior.
1. Your pull request should be comprised of a squashed commit if there are several commits that are working to the same end. 

## Checklist:

- [ ] Clone local copy of the repo
- [ ] Cut work branch off of sprint (don't cut new branches from existing feature brances)
- [ ] Follow the correct naming convention for new branch
- [ ] Branch is focused on a single main change
- [ ] All changes/commits directly relate to this main change
- [ ] Rebase the origin sprint branch after main change is made
- [ ] Run the tests
- [ ] Push cut branch 
- [ ] Make pull request from remote repo's cut branch sprint branch
- [ ] Write a clear pull request message detailing what changes were made
- [ ] Get a code review
- [ ] Make any requested changes from that code review
- [ ] After QA approval, merge code and delete feature branch

<!-- Links -->
[curriculum workflow diagram]: http://i.imgur.com/p0e4tQK.png
[cons of merge]: https://f.cloud.github.com/assets/1577682/1458274/1391ac28-435e-11e3-88b6-69c85029c978.png
[tools workflow diagram]: http://i.imgur.com/kzlrDj7.png
[Git Flow]: http://nvie.com/posts/a-successful-git-branching-model/
[GitHub Flow]: http://scottchacon.com/2011/08/31/github-flow.html
[Squash]: http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html
