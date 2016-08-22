[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Using Git for Version Control

<!--
  title: Using Git for Version Control
  type: lesson
  estimated duration: 120 min
  creator: Matt Brendzel
  competencies: git, GitHub
-->

## Objectives

  At the end of this session, you should
  (with the help of a reference, and a little time)
  be able to:

  - View a detailed history of the commits in a repo.

  - Use Git to visit old commits and see previous states of files.

  - Define branches and travel to them.

  - Fix your commit history by...

    -   rewriting a bad commit message,
    -   reverting some set of uncommitted changes made since the last commit,
    -   stashing uncommitted changes,
    -   resetting (permanently) the state of the repo to a prior commit, and
    -   restoring a local repo's branch from a remote repo (e.g. GitHub).

## Prerequisites

  You should already be able to:

    - Create a new Git repository.
    - Add and commit changes.
    - Build a static HTML page.

## Git, the Time Machine

<!-- est 5 mins -->
### [Read: Explore Git History](./readings/git-history.md)

<!-- est 15 mins -->
### Code Along: Explore Git History

  We're going to use `git log` and its many different options flags to look
  at a repository's history.

  1.  Please clone [this repository](https://github.com/EnterpriseQualityCoding/FizzBuzzEnterpriseEdition)
      to your local desktop.

      > We aren't forking it this time, just cloning it. Why?
      > Because we won't ever be pushing code back. That's the only reason why
      > forks exist - to give you a copy of a repo that you can control (i.e.
      > push changes to).

  2.  Let's view the history of this repository using `git log`.

  3.  Let's use `-n` flags to show only the last 'n' commits.

      -   `git log -n 3`
      -   `git log -3`
      -   `git log -n 9`

  4.  Next, let's combine it with the `-p` flag to show the actual changes from
      the last 'n' commits along with the commit messages.

      -   `git log -p -n 3`
      -   `git log -p -2`
      -   `git log -n 3 -p`

  5.  Now let's swap the `-p` flag for the `--stat` flag, so that we see stats
      _about_ the changes, rather than the changes themselves.

      -   `git log --stat -4`
      -   `git log -2 --stat`

  6.  This time, let's exchange `--stat` with `--oneline` to get an even more
      truncated output.

      -   `git log --oneline -3`
      -   `git log -2 --oneline`

  7.  OK, let's change thigns up. Instead of changing out `--oneline`, let's
      replace the `-n` flag(s) with the `--since` flag, so that we can see all
      commits made after a specific date/time.

      -   `git log --oneline --since "2016-08-21"`
      -   `git log --oneline --since "2016-08-12T16:36:00-07:00"`
      -   `git log --oneline --since "2 days ago"`
      -   `git log --oneline --since "2 days ago"`
      -   `git log --oneline --since "2 weeks 3 days 2 hours 30 minutes ago"`

      Using the related flag `--until` lets you see commits made _before_ a
      specific date/time. You can also use the aliases `--before` and `--after`
      instead.

      -   `git log --oneline --until "2 days ago"`
      -   `git log --oneline --before "2 days ago"`
      -   `git log --oneline --after "2 days ago"`

  8.  Let's try out a couple more `git log` flag combinations:

      -   `git log --oneline --decorate`
      -   `git log --oneline --decorate --all`
      -   `git log --oneline --grep '...'`

<!-- est 5 mins -->
### [Read: Visit Past Commits](./readings/time-travel.md)

<!-- est 15 mins -->
### Code Along: Visit Past Commits

  1.  Create a new directory called `story`, and turn it into a repo by running
     `git init`.

  2.  Inside `story`, create a new file called `chapter-1.txt` using the `touch`
      command.

  3.  Let's write a short story in this repo together!
      Add each sentence below to `chapter-one.txt`, one at a time, and make a
      commit after each addition.

      > Once upon a time, there was a young woman with long golden hair.
      > People called her 'Goldilocks'. People were not very creative.
      >
      > One day, while this girl was going for a walk in the forest, she came
      > upon a worn-down hovel situated in the middle of the deep woods.
      > Goldilocks, never one to leave something be, decided that maybe
      > breaking and entering wasn't _really_ so bad as long as the place seemed
      > abandoned.
      >
      > She walked up to the large wooden door and began to
      > pull on the handle, but the door was stiff and heavy, and
      > wouldn't budge. "Of all the days to leave my crowbar at
      > home...", she muttered.

  4.  Now that we have a few commits, let's look at them using the `git log`
      command. To make our view easier to read, let's use the `--oneline` flag.

  5.  See how each commit has a different SHA id? Let's pick one of those commits,
      jot down the first six characters of its id, and jump over to it using
      `git checkout`. If we open `chapter-one.txt`, the content will have changed!

  6.  Run `git log --oneline` to see the commits leading up to the present one.
      Let's pick another commit and jump to it, using its SHA code.

  7.  We can go to the most recent commit by running `git checkout master`.

  8.  Create a file called `chapter-2.txt` -- we're going to add a new chapter
      to our story. This time, we'll only make one new commit.

      > Having utterly failed to move the heavy door, Goldilocks tried the
      > windows next. One on the side of the house was un-rusted enough to move
      > when she lifted it; she grabbed onto the sides of the window and started
      > pulling herself in.
      >
      > After an unceremonious landing on the floor inside,
      > Goldilocks stood up, brushed herself off, and immediately began looking
      > around the room she'd entered. What she saw was a mess of overturned
      > tables and chairs, a fireplace that had long been empty, and -- perhaps
      > most curiously -- a severed stag's leg. "Huh", was all she said.

  9.  Instead of looking up a commit in the log, we can tell Git to check out a
      specific commit based on its relative position to `HEAD` a reference that
      points to wherever you 'are' within the history of the repo. To go to the
      commit before `HEAD` (i.e. to backward in time by one commit), you can
      type `git checkout HEAD~1`. This will work with any number you give it.

  10. See how `chapter-2.txt` has disappeared? In addition to adding or removing
      changes within a file, Git can also add or remove entire files, and even
      whole directories of files.

      <!--
      [Aside]
      "Although Git can do this to files, it cannot do this to directories.
      Git works by tracking all the files in your project, but directories are
      always ignored. Because of this, if you want Git to be aware of an
      otherwise empty directory, you will usually create a hidden file
      (traditionally called `.gitkeep`)".
      -->

<!-- est 15 mins -->
### Do: Visit Past Commits

  Create a new repo called `directions`, with a text file in it called
  `nypenn-to-central-park.txt` Add each of the following lines to that file,
  one at a time, and make a commit after each addition.

  > DIRECTIONS: NY Penn Station to Central Park
  >
  > 1: Walk north on 7th Avenue to 34th Street.
  >
  > 2: Turn right on 34th Street and walk until you reach Avenue of the
  >    Americas.
  >
  > 3: Go to 34th Street Station - Herald Square and board the northbound F
  >    train.
  >
  > 4: Ride the F train for three stops, and get out at the 57th Street
  >    station.
  >
  > 5: Continue walking north on Avenue of the Americas until you reach Central
  >    Park.
  >

  Once you've made these commits, use `git log` to review the commit history.
  Try to navigate backward one commit at a time, starting from the most recent,
  until you get back to the first commit. When you've finished,
  run `git checkout master` to get back to the last commit.

<!-- est 10 mins -->
### [Read: Reference Commits with Branches](./reading/branches.md)

<!-- est 10 mins -->
### Code Along: Reference Commits with Branches

  Let's revisit the `story` repo from the previous code-along exercise.

  1.  Let's create a new branch called `possible-ending`, and check it out.
      When we run `git log --oneline --decorate`, both branches will be visible.

  2.  Let's make some new commits on this branch, just like we did before,
      adding the story below, line by line, to `chapter-2.txt`.

      > Goldilocks didn't have a lot of wilderness experience, but seeing the
      > leg of a rather large animal lying on the ground suggested to her that
      > there must be an **even larger** animal around somewhere that tore it
      > off in the first place.
      >
      > With that realization, Goldilocks straightened up, turned right around,
      > and made a bee-line back to the window she came in through.
      >
      > After hurriedly forcing herself through the window and running back from
      > the house to the forest path, there was only one thought on her mind.
      > "This was an incredibly stupid idea."

  3.  Run `git log --oneline --decorate` again, and look at the output. How have
      things changed?

  4.  Check out the grandparent of the present commit (`HEAD~2`).

  5.  Stop! Before moving on, let's create and check out a new branch called
      `alternate-ending`.

  6.  On our new branch, let's write a different ending to the story from the
      version on the `master` and `possible-ending` branches.

      > Goldilocks walked up close to the stag's leg to try
      > and get a better look.
      > "Hmm", she thought, "Someone's on the Paleo diet."
      >
      > It looked like the leg wasn't very fresh, so whoever had
      > brought it in must have done it a little while ago.
      > Goldilocks, taking this as a cue to keep exploring,
      > made her way from the main room to another, smaller room in the back...

  7.  After we've made a few commits, let's look at the commit logs again with
      `git log --oneline --decorate`. How have they changed?
      Let's try adding the `--graph` flag to our `git log` command. Do we see
      anything different?

<!-- est 10 mins -->
### Do: Reference Commits with Branches

  Let's make some modifications to the `directions` repo from earlier.

  1.  Check out the commit that adds step 2 of the directions ("Turn right on 34th
      Street...")

  2.  Create a new branch starting at that commit called `empire`.

  3.  Change the first line of `nypenn-to-central-park.txt` to say 'the Empire
      State building' instead of Central Park. Then, rename the text file itself
      to `nypenn-to-empire-state-bldg.txt`.

      > Hint: You'll have to use a special variation of `mv` in order for Git to
      > properly recognize the change.

  4.  Add both of the following directions to the file, one at a time, and make a
      commit each time:

      > 3: Walk south to 33rd Street.
      >
      > 4: Enter through the east entrance, on Avenue of the Americas.

  5.  Run `git log --oneline --decorate --graph`, to see the current structure of
      the commit history.

  6.  Jump to the `master` branch, and make a commit after adding the following
      line to the end of the textfile:

      > Congratulations, you are now in Central Park!

  7.  Jump back to the `empire` branch and run the `git log ...` command again.

<!-- est 5 mins -->
### [Read: Fix Commit History](./fixing-history.md)

<!-- est 15 mins -->
### Code Along: Fix Commit History

  Let's see how we can handle errors in our commit history, once again using the
  `story` repo from earlier.

  1.  We'll start by checking out the `alternate-ending` branch, adding
      the following text, and make a commit.

      > As she poked her head through the door, she saw
      > three enormous bears sleeping against the far wall.
      > "I", she thought, "have made a terrible mistake."

  2.  Suppose that we made a mistake in our commit message in that last commit
      -- maybe it wasn't detailed enough, or had some incorrect information
      This last commit isn't (yet) shared publicly yet, and since it's at
      the end of the branch, no other commits reference it, so it should
      be safe to redo the commit.
      Run `git commit --amend` to replace your previous commit with an
      almost-identical (different SHA code) new commit, and write in your
      corrected commit message.

  3.  OK, new scenario. Let's add a whole bunch of random
      nonsense into `chapter-2.txt`, in random locations -- simulating, perhaps,
      a cat discovering that your keyboard is a delightful place to nap
      -- and save the file.

  4.  >  Bad kitty! Out!

      Run `git add chapter-2.txt`, followed by `git checkout HEAD`;
      this will stage the new changes, causing Git to destroy them when a new
      commit gets checked out.

      Remember, this will completely obliterate **all** changes to that file more
      recent than the last commit. Use with caution!

  5.  Let's make another change to the story, but not commit it.

      > "I", she thought, "have made a _dreadful_ mistake"

      Suppose that we wanted to switch to the `possible-ending` branch,
      but weren't ready to make an entire new commit for just that one small
      wording change. If we run `git add chapter-2.txt` and `git stash`,
      we can temporarily save those changes, and then add them back later.

      Let's test this out by checking out `possible-ending`, checking out the
      `alternate-ending` branch again, and putting back those stashed changes
      using `git stash pop`. Once the changes are back, let's make a commit.

  6.  You know, after a second reading, the first version of that last
      line was better. Let's permanently revert to the previous version
      by typing `git reset --hard HEAD~1`.

  7.  So far we've only been working with a local repo. Let's create a
      new empty repo on GitHub, and push up code from all three of our
      branches (`master`, `possible-ending`, and `alternate-ending`)

  8.  Delete the `alternate-ending` branch:
      `git branch -d alternate-ending`

  9.  Restore the deleted branch by running
      `git checkout alternate-ending`;
      this creates a local tracking branch called `alternate-ending` which
      mirrors the `alternate-ending` branch of the GitHub remote.
