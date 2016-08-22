[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Fixing History

OK, let's face facts for a minute. You are basically guaranteed to have at least
one "oh $#!%" moment with Git. Fortunately, Git has some tools that allow us to
deal with these situations when they arise.

## "Oh $#!%" Situation 1 : Bad Commit Message

Maybe it's too short. Maybe it's too long. Maybe it has a horrible, embarassing
typo. Or maybe it's just not accurate. For any number of reasons, developers
often find themselves in the position of needing to fix the commit they just
made. Thankfully, Git has a tool for just this purpose, the `--amend` option
for `git commit`.

If your commit history looks like this,

```bash
788139b (HEAD -> master, origin/master, origin/HEAD) Finnish tests
e51129c Add tests for first feature
903a1be Make a README
```

and you want to make it clear that your tests are not from Finland, just run
`git commit --amend` -- it will open up your text editor, allowing you to
rewrite the commit message. In the end, your history will look like this.

```bash
9fe7a6b (HEAD -> master, origin/master, origin/HEAD) Finish tests
e51129c Add tests for first feature
903a1be Make a README
```

Wait wait wait. Hold up. That's not the same SHA that was there earlier. What's
up with that?

> `788139b` ==> `9fe7a6b`

Well, we weren't just changing the commit message when we used `--amend` -- Git
was creating an entire new commit. This isn't a problem if you're at the end of
a branch (and if the original commit hasn't been publicly shared yet), because
nothing other than the branch itself refers to that commit.
**NEVER, _EVER_** use `--amend` on a commit that's referenced by someone or
something -- it will cause those references to break, potentially destroying all
of someone's work.

## "Oh $#!%" Situation 2 : Discarding a Failed Experiment

Suppose that after the last commit, you did some experimenting in order to try
something new. Unfortunately, not only was the experiment unsuccessful, you
ended up breaking your code in the process. How do you get back to the last
working version (i.e. the final commit)?

If we were to use `git checkout` to go back to the most recent commit
(referenced) by `HEAD`, Git would restructure the file system and files to be
exactly the same as they were when that commit was made.

However, the unstaged changes would remain unstaged, even as you checked out
other commits. In order for Git to discard those changes, it needs to have a
record of them, and for that you need to use `git add` to stage them all; then,
once all of the changes you want to get rid of are staged, use
`git checkout HEAD` to roll back the state of the repo to before your experiment
took place.

## "Oh $#!%" Situation 3 : Writing Code on the Wrong Branch

Sometimes, you think you're working on one branch, but you're actually on
another. You obviously don't want to commit code in the wrong place. How can it
be ferried from one branch to another?

Git has a built in tool called the _stash_, which allows you to store sets of
changes, independent of any commit. To use it, stage (using `git add`) all of
the changes that you want to "stash", and then run `git stash`; all of those
staged changes will get stashed.

Once you've stashed the code, all you need to do is check out the correct branch
and run `git stash pop` to bring those previous changes out of cold storage.
Once that's done, the changes can be staged and committed, as usual.

Stashed data is stored in a type of [data structure](https://en.wikipedia.org/wiki/Data_structure)
called a [stack]().
We'll learn more about stacks (and other data structures) in the future, but for
now, the important takeaway is that the stash is 'LIFO' -- last-in/first-out.
What this means in practical terms is that the last set of changes you stash
will be the first thing that comes out when you run `git stash pop`.

## "Oh $#!%" Situation 4 : Needing to Completely Destroy Commits

Let's say that you commit a file that you shouldn't have, and you need to
completely annihilate that commit. Git has a way of forcing a roll-back to a
prior commit: the `--hard` flag on `git reset`. If you wanted to completely wipe
out the most recent commit, and go back permanently to the one before it, you
could write `git reset --hard HEAD~1`.

However, this is a very dangerous tool if misused, since it will permanently
alter your commit structure.

## "Oh $#!%" Situation 5 : Ummm... where did my branch go?

You deleted it. Or renamed it. Or something. In any case, it was there before,
and now it's not. What can you do?

Well, hopefully, you have a backup. One common approach is to regularly push all
or nearly all important branches up to GitHub -- that way, they're retrievable.

Supposing that you did need to retrieve a branch from a remote repo, you can
use the command `git checkout some-branch --track origin/some-branch` to create
a new branch on your repo that 'tracks' (i.e. mirrors) a branch on the remote
repo. This command can also just be shortened to
`git checkout origin/some-branch` if both branches have the same name, and to
`git checkout some-branch` there is only one branch across all remote repos with
that particular name.

## Etc

The [Git documentation](https://git-scm.com/doc)
has a [handy page on undoing changes](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)
-- it might be worthwhile to bookmark it.

[< Back](../README.md)
