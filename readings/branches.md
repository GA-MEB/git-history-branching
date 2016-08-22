[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Branching

In the last reading, we saw that it was possible to check out any commit in the
repository's history by typing `git checkout` followed by that commit's SHA.
However, even this can be tricky. For instance, you can always see earlier
commits' SHAs by typing `git log`, making moving backwards in time fairly easy.
You can also use `~` to move backwards in time from the current state of the
repo. However, `git log` does **not** show more recent commits, so it's not
possible to just look up the SHA -- you would need to have written it down --
and `~` only works in one direction.

In the previous exercise, when we wanted to move forward in time again, we typed
`git checkout master`.

> "Whats up with that? Don't we need to give `git checkout`
> a commit's SHA, or a relative reference like `HEAD~2`?
> What the heck actually is `master` anyway?"

`master` is an example of a **branch** -- a moveable reference to a specific
commit. It's easy to see how branches make it simpler to navigate our commits.
However, it's important to recognize that checking out a branch is _not_
quite the same as checking out the commit directly. The reason for the is that
when you check out a branch, and then make a commit, Git does something
interesting: it changes the location of the branch to point at the new commit,
rather than the old one.

-   Before the commit:

    ```plaintext
    > git log --oneline --decorate

    788139b (HEAD -> master, origin/master, origin/HEAD) Add first feature
    e51129c Add tests for first feature
    903a1be Make a README
    ```

    > This log is also showing where the branches on our remote repo, `origin`,
    > fit within the commit tree.

-   After the commit:

    ```plaintext
    > git log --oneline --decorate

    a4e77cc (HEAD -> master) Add tests for second feature
    788139b (origin/master, origin/HEAD) Add first feature
    e51129c Add tests for first feature
    903a1be Make a README
    ```

    > Notice how `master` now points to a different commit than `origin/master`?
    > Our local repo is out of sync with our remote repo. We can fix this by
    > "pushing" commits from our local `master` branch to our remote `master`
    > branch.

Although the chain of commits gets longer and longer as we make more commits,
`master` will always refer to the last commit in the chain. In a sense, `master`
represents the entire 'timeline' of commits, tracing back all the way to the
initial commit -- that's why it's called a "branch"!

To create a new branch, we can write `git branch` followed by the name of the
new branch. Or, to create _and_ check out a new branch all at once, we can write
`git checkout -b` followed by the name of the new branch.

> "OK, that's interesting, but it doesn't explain why we could only look
> backwards in the first place. What's up with that?"

The answer to that question has to do with the the architecture of Git itself.
Every commit has a few properties: a collections of changes (additions and
subtractions), an SHA, a time when it was created, a commit
message, and... a reference to the previous commit. That's it (mostly).

Although each commit is only aware of one other commit, when you start
at the commit all the way at the end, it's possible to trace your way
all the way back to the initial commit.
So what refers the commit at the end? Ideally, a branch. If for whatever
reason there weren't anything referring to that commit, the only way to
reach it would be using its SHA code.

> This is a pretty bad scenario, and one to try to avoid.
> We'll look at how to fix this in the 'Oh Crap' section
> of the lesson.

Here's one common situation where this can happen. Say that you want to check
out an old commit, not just to view it, but to actually make a new commit on top
of it. You check out the commit, begin working, and make a commit on top of the
commit you checked out. So far so (apparently) good! However, because you
checked out a commit rather than a branch, you're not currently on a branch
either. this means that if you were to check out the `master` branch, there'd
be no way back to the work you just did (apart, obviously, from referencing it
by its SHA).

How can this be prevented? Simple! Just create and check out a new branch at any
point in the process after you check out the old commit. Once you create the
branch, all prior commits become reachable from that branch, and all future
commits will be made _on_ the branch. In fact, it's not a bad idea to simply
create and check out a new branch right away, as soon as you've gone back to the
old commit -- that way you won't forget.

e.g.

```bash
git checkout HEAD~6              ## Or use the SHA
git checkout -b my-new-branch
```

[< Back](../README.md)
