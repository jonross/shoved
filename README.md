# What is it?

`shoved` is a stronger `pushd`.  In addition to the features offered by `pushd` and `popd`, it has

* Directory listing uses `dirs -v` by default, which is more readable
* Aliases for commonly used directories
* Custom alias substitution
* Prologue and epilogue hooks

# Usage

## Setup

Copy `shoved` to a directory in your path (`make install` will put it in `~/bin`) and run

    eval "$(shoved setup)"

## Basics

`dl` gives the directory list.  `dp DIR` does `pushd DIR`.  `dp` without args does `popd`.

    % cd
    % dl
     0  ~

    % dp /tmp
     /tmp
    % dp /etc
     /etc
    % dl
     0  /etc
     1  /tmp
     2  ~

    % dp
     /tmp
    % dl
     0  /tmp
     1  ~

`dx` does `pushd` -- exchanges the top two directories.

    % dp /etc
     /etc
    % dl
     0  /etc
     1  /tmp
     2  ~
    % dx
     /tmp
    % dx
     /etc

`d N` or just `N` does `pushd +n` -- goes to the Nth directory in the list.

    % dl
     0  /etc
     1  /tmp
     2  ~
    % d 2
     ~
    % dl
     0  ~
     1  /etc
     2  /tmp
    % 1
     /etc

## Shorcuts

You can set up short names for commonly used directories; these are understood by `d` and `dp`.
`dn NAME` sets the short name for the current directory to NAME; `dn` displays the shortcuts.

    % dn
    /Users/jross/.shoved.names not found
    % cd /usr/local/bin
    % dn ulb
     ulb  /usr/local/bin
    % cd /tmp
    % d ulb
     /usr/local/bin
    % pwd
    /usr/local/bin
    % dp /usr/local/lib/python2.7
     /usr/local/lib/python2.7
    % dn pylib
     pylib  /usr/local/lib/python2.7
    % dn
     pylib  /usr/local/lib/python2.7
     ulb    /usr/local/bin

These are stored in `~/.shoved.names`, which is a plain text file you can edit.

## Custom callbacks

You can inject your own logic by setting the `SHOVED_HELPER` environment variable to an executable
script.  It will be invoked as

    yourscript resolve DIR

whenever you run `d DIR` or `dp DIR`.  It should output an actual resolved directory, or nothing
if you want normal pathname resolution.  It will also be invoked as

    yourscript enter DIR

whenever your working directory changes.  In this case, you should output additional commands to
be run before the directory change command returns.

## Other

`ds` is a shortcut for `eval "$(shoved setup)"`

`shoved version` shows the script version
