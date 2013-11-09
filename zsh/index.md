/*
Title: ZSH Snippets
Description: Various ZSH stuff
Date: 2013/10/27
Tags: bash,sh,zsh
*/

So here I will be sharing some commands I often use myself.

For an exhaustive list, see [grml.org](http://grml.org/zsh/zsh-lovers.html "grml.org | zsh-lovers")

## BangBang!

    # touch test; exit
    $ echo "test" > test
    > zsh: permission denied: test
    $ sudo !!; cat test
 
## Repeat last argument

    $ touch "very long filename That You Do Not wanna repeat"
    $ echo "test" > !$; cat !$
    > test

## Redirect stdout with sudo

    # touch test; exit
    $ echo "test" > test
    > zsh: permission denied: test
    $ sudo !!
    > zsh: permission denied: test
    $ sudo su -c 'echo "test" > test'; cat test
    > test

## Heredoc to file

    $ cat <<EOM > test; cat test
    heredoc>okay
    heredoc>now stop!
    heredoc>EOM
    > okay
    > now stop!

`EOM` (End Of Message) is just a _randomly_ chosen stop parameter. Just remember: do not put a space char after `<<`.
 
