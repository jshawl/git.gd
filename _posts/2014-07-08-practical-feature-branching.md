---
layout: post
---

When I first started using git, I never used branches. My typical workflow was more or less:

1. `git pull origin master`
2. make some edits
3. `git add .`
4. `git push origin master`

ad infinitum.

This workflow worked well for me until I started working with teams and larger clients
with staging and production servers.

I remember one day I was working on a project with a git log like:

    * e55c976  (HEAD, master) 1 day ago Jesse Shawl
    |  Important bugfix that should be deployed immediately
    * f158085  2 days ago Jesse Shawl
    |  worked on experimental feature
    * eb945d6  (origin/master) 3 days ago Jesse Shawl
    |  ready for deploy; all tests passing
    * e29e182  6 weeks ago Jesse shawl
    |  initial commit

I can't just `git push origin master`, because that would deploy my not-yet-ready
work on the experimental feature. Lesson learned: I should have used a feature branch to keep master
in a deployable, always production-ready state.

That's ok though. It's possible to retroactively create the feature branch and deploy
the important bugfix.

First, create a new `feature-1` branch, and base it off of the relevant commit.

    $ git branch -b feature-1 f158085

Then, delete the feature-1 related commits from the master branch:

    $ git rebase -i origin/master

You'll see a list like:

    pick f158085 worked on experimental feature
    pick e55c976 Important bugfix that should be deployed immediately
    
Just delete the lines that you don't want -- in this case the first one, and save and quit the file.

The ouput of `git log` should look something like:

    * e55c976  (HEAD, master) 1 day ago Jesse Shawl
    |  Important bugfix that should be deployed immediately
    | * f158085  (feature-1)  2 days ago Jesse Shawl
    |/   worked on experimental feature
    * eb945d6  (origin/master) 3 days ago Jesse Shawl
    |  ready for deploy; all tests passing
    * e29e182  6 weeks ago Jesse shawl
    |  initial commit

Now I can deploy my master branch. When I'm ready to continue working on the 
experimental feature, I just need to switch to the `feature-1` branch:

    $ git checkout feature-1

