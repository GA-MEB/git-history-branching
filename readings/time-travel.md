[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Visit Past Commits

## i.e. Git, the Time Machine

In the previous reading, we mentioned that commits were important because of the
commit messages -- they allow us to create documentation for our app as we build
it. However, this is not the real reason

We've been referring to Git as a "version control system", but so far we haven't
really seens anything for managing different versions of our project.

That changes now. We're about to get into the core functionality of Git --
moving around between different commits.

**"Moving around? What does that mean?"**

Well, commits aren't just collections of changes with custom labels. Each commit
represents an incermental change -- a _**differential**_ -- from the prior state
of the repository. If you add up all of these differentials, you end up with the
current state of the repository. However, if you only added up _some_ of the
differentials, you would end up with the state of the repository
_when the last commit was made_. By choosing how many of these differentials you
get applied, it's essentially possible to change the state of the repository to
what it looked like after _every commit in the history of the repo_.

The command that Git uses to accomplish this is `git checkout`. Remember that
SHA thing from the previous reading? That code is a unique identifier for a
particular commit.

```bash
commit c66f4434200720269ca82a6dff817e0a93763949
Author: Boaty McBoatface <btmcbtfc@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Remove unnecessary test

commit b3bcb608e1e84085b51d4b2432f8ecbe6306e7e7
Author: Boaty McBoatface <btmcbtfc@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    Create boilerplate

commit 402fe7563abf99a11bef06a3f659ad00de2209e6
Author: Boaty McBoatface <btmcbtfc@gee-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700

    First commit
```

If we wanted to go 'back in time' to the commit labeled "Create boilerplate",
all we would need to do is write `git checkout` followed by the SHA for that
commit. e.g. `git commit b3bcb608e1e84085b51d4b2432f8ecbe6306e7e7`

This is really long. Fortunately, seven alphanumeric characters are almost
always enough to uniquely identify a commit (36^7, or 78,364,164,096, possible
sequences), so it's generally acceptable to write just the first seven
characters of the SHA when you're referencing a commit.
e.g.  `git commit b3bcb60`

If you were to do this, and then look inside the repo, you would see that files
and folders would all be set up like they were back when that commit (`b3bcb60`)
was made.

[< Back](../README.md)
