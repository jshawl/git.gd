---
layout: post
---

I've heard about [hub](https://hub.github.com/) a few times before now but have not yet tried it out.

It's a command line wrapper around `git` to facilitate working with github. I came across hub
again recently when I was looking for an easier way to clone my repos. i.e. I don't wan't to have to
type `git@github.com:jshawl` everytime I clone a new repo.

It would be nice to clone repos like:

- `$ git clone vanilla` => `git clone git@github.com:jshawl/vanilla`
- `$ git clone jekyll/jekyll` => `git clone git@github.com:jekyll/jekyll`

and of course work with regular urls as well:

- `$ git clone git@bitbucket.org:jshawl/vanilla.git`

Fortunately, hub does all this, and more!

The first step is to install hub with `brew install hub`. [Homebrew](http://brew.sh/) is a package manager
for Mac OS X.

After the install, I tried cloning my first repo with the hub command:

    $ hub clone vanilla

Immediately, I was prompted to enter my username and password, which
means hub is translating the remote url to use the https protocol
instead of the password-less ssh protocol.

According to the [clone feature spec](https://github.com/github/hub/blob/e807a3891b13a45d52447b63ca4e54c25a78dc13/features/clone.feature#L112-L114):

    When I successfully run `hub clone dotfiles`
    Then it should clone "git@github.com:mislav/dotfiles.git"
    And there should be no output

I also found [this issue](https://github.com/github/hub/issues/581) which says
authentication with the GitHub API via ssh key is not possible :(

I think for now, I'm going to stick with typing out the url and not using hub
because I don't want to have to deal with passwords.

This might be convenient, though if you have multiple github accounts and need to specify
on a repo-by-repo basis which user has access.

Lastly, this is inspiring me to write my own wrapper for git! I don't need the full-blown
github functionality, just a url translator.

