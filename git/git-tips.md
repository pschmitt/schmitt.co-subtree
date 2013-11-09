/*
Title: Git Tips&amp;Tricks
Description: Various Git Tips 
Author: Philipp Schmitt
Date: 2013/10/26
Tags: git,github,submodule
*/

In this post, I will go over a few FAQs about Git. I'm an ArchLinux user, so I'm using the very latest stable Git (1.8.4 as I am writing this). Keep this in mind as some of the listed commands may not work with older versions.

# Submodules

If you do not know what this is read [this](http://git-scm.com/book/en/Git-Tools-Submodules "Git Submodules").

**TL;DR**: Submodules are _somehow_ Git's equivalent to SVN externals 

## Add a new submodule

    $ git submodule add ${URL} ${DIRECTORY}

Note that `${DIRECTORY}` is optional but comes in handy if you want to add a repo to a folder that has a different name than the said repo.

## Remove a submodule

    $ git rm ${submodule_path}  

If you are using Git 1.8.5+ this should be it. If your are stuck with an older version, you may need to manually edit `.gitmodules` and remove the line corresponding to the submodule you want to remove.

## Clone including submodules

By default, `git clone` does not clone submodules. If you wish to do this, a simple...

    $ git clone --recursive ${REPO}

will do the job.

## Update all submodules

    $ git pull
    $ git submodule update --init --recursive
    $ git submodule foreach --recursive git fetch

## Pushing to a submodule

Well, first off make sure you initialized your submodules (`git submodule init`) and that you are on a branch:
    
    $ cd ${submodule}
    $ git status
    > # HEAD detached at 5ff339b

In this case we are not on a branch. Don't panic we can make this right with:

    $ git checkout master

Obviously you need to adjust `master` to the branch you want to check out.

## Forgot to checkout a branch ?

Sh!t happens, luckily enough you won't lose anything if you do a checkout. Remember to commit your changes though.

    $ git commit -am "Awesome new feature"
    > [detached HEAD c92741d] Awesome new feature
    >  1 file changed, 1 deletion(-)
    $ git checkout master
    $ git cherry-pick c92741d
    $ git push

## Submodules: SSH vs. HTTPS

Submodules are great, but when it comes to sharing stuff with other people on GitHub, things may get tricky. As you may know, the _HTTPS_ protocol allows anonymous clones, but _SSH_ relies on key authentification. Dilemma: should I use _HTTPS_ for *ALL* my submodules, even if this requires password:username input for every `git push` ? Should I set a *huge* timeout for HTTPS Auth ?

Nope: there is a magic trick that allows you to use _HTTPS_ for your submodules and still use the _SSH_ when you are pushing your changes to the remote. Just add the following to your `~/.gitconfig`:

    [url "git@github.com:${USERNAME}/"]
        pushInsteadOf = "https://github.com/${USERNAME}/"

Don't forget to change ${USERNAME} to your username.

Source: [pbrisbin | Git Submodule Config](http://pbrisbin.com/posts/git_submodule_config/ "Git Submodule Config") 


# Undoing stuff

## Change your last commit message (_prior_ to pushing!)

This one is easy. Try this:

    $ git commit --amend -m "New commit message"

Source: [stackoverflow | How do I edit an incorrect commit message in Git?](http://stackoverflow.com/a/179147/1872036 "How do I edit an incorrect commit message in Git?")

## You pushed a file containing a password, your credit card info, or the reset code for the internet to a public repo

1. Do never, ever, ever do this again
2. Consider killing yourself
3. Read [this](https://help.github.com/articles/remove-sensitive-data "GitHub | Remove sensitive data")
4. Use a `.gitignore` file next time

# Misc

* Do **NOT** use a GUI-wrapper (like turtoiseGIT, eclipse ...)
