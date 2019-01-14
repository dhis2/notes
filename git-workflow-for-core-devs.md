# Git workflow for core devs

The cheat sheet that you can find on this repo's README
already provides enough information so you can get started.

There are a few downsides though if you're following that quick guide.
As we're supporting the last three released versions, some issues will
have older versions as a target.

If you follow the cheat sheet, your workflow after finishing the issue
on the master branch might be: checkout the older version branch,
cherry pick your changes and you're kind of done.
[This might result in a lot of trouble](https://blogs.msdn.microsoft.com/oldnewthing/20180312-00/?p=98215)

# A better start

Before you start working on a ticket, you should check which target versions
are mention in the JIRA ticket.

Now you can find the merge base of the target versions.
If the next release version is 32 (master branch) and you'll have to support
v2.30 and v2.31 as well, just get the merge base with the following command:

```bash
# Some repositories might use something else as branch name, e. g. v2.31
# Just replace the v31/v30 names in the following command
$ git merge-base master v31 v30
```

This will return a commit hash that you simply checkout,
and from which you can create the actual feature branch, e. g.:

```bash
$ git merge-base master v31 v30
=> 302018338b02321b889f9018660300fd43311df5 

# This will tell you that you're in detached mode,
# but as you'll create a branch anyways, you won't need to worry about that
$ git checkout 302018338b02321b889f9018660300fd43311df5
$ git checkout -b DHIS2-1337_A_good_branch_name
```

If you now start developing on this branch, it'll be way easier
to merge everything into the versioning branches.

# Name your feature branch correctly

In order to make JIRA and Github play nicely together,
start your branch's name with the ticket ID, e. g. `DHIS2-1337`.

Prepend the ticket ID with a meaningful, but not too long name,
that describes which changes will be introduced by your branch.

# Commit message convention

There are docs for this in the general docs as this is not really
front end specific. You can find them here:

[Packages and style conventions](https://dhis2.github.io/blog/2018/12/07/packages-and-conventions.html)

# Save your changes on a granular level

It obviously makes sense not to clutter the master/version branches
with you dev commits, so you might be thinking about squashing your
work of the day before pushing your branch to github.

You don't need to do that as we're squash-merging the pull request anyways.
When merging your branch after it being approved by another developer,
you'll be asked to provide a squashed merge commit message.

This means that you can push your branch at any time without having to 
worry about the commits that you'll make during development. There might
be a chance that you'll need your commits to be small in the future,
just for reverence or so.

# Cleanup after your branch has been merged

It's common sense to clean up the repository and only keep the branches
that haven't been merged yet or will be needed again.

Once you've merged your branch, you'll be given the option to delete
your remote branch on github. Normally you should be able to just delete
your branch, so do it. Otherwise please keep in mind that your branch is still
on the remote repository, no one is going to delete that branch for you.

You should never work on a branch that has been merged already.
If a ticket returned because didn't pass the review, create a new branch with
the same ticket id and an updated description that reflects what you'll do on
that branch. This means that you can also delete your local branches once
you've merged your pull request.
