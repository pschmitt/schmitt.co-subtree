/*
Title: sed Snippets
Description: Various sed stuff
Date: 2013/10/27 
Tags: sed,bash,sh,zsh
*/

## Basic sed usage

The stream editor is your go-to-guy to alter text files:
    
    $ echo "matchme matchme matchme matchme" | sed -e 's/matchme/matched/g'
    > matched matched matched matched

This command replaces (`s/`) all (`/g`) occurences of `matchme` by `matched`.

## Usefull flags

`-i`: Operate on a file directly
    
    $ echo "matchme matchme nomatch matchme" > test
    $ sed -ie 's/matchme/matched/g' test; cat test
    > matched matched nomatch matched

## sed as grep alternative

Most people would simply pipe grep's output into sed for further processing, like this: 
    
    $ grep something file | sed -e 's/string/replacement/' > file

But there is a simpler way of achieving this:
    
    $ sed -ie '/something/s/string/replacement/' file

## Multiple commands

    $ sed -e 's/matchme/matched/g;s/match2/matched2/g' <<< "matchme matchme nomatch nomatch match2 match2"
    > matched matched nomatch nomatch matched2 matched2 
