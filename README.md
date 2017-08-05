# Setup

Copy `shoved` to a directory in your path (`make install` will put it in `~/bin`) and run

    eval "$(shoved aliases)"

# Basics

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

# Directory shorcuts

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
