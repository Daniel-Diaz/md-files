# Getting Haskell in Linux

By _Haskell_ I mean _GHC_ and _cabal-install_, not the
[Haskell Platform](https://www.haskell.org/platform).

## Assumptions

Your Linux distribution includes the following commands:
`apt-get`, `wget`, `tar`.

## GHC

### Prerrequisites

* `apt-get install make`
* `apt-get install libgmp3-dev`

### Getting

GHC can be downloaded from the [GHC site](http://www.haskell.org/ghc/download).
Choose a version (you might want _current stable release_). Then choose
a supported platform (probably *Linux (x86_64)*). Download and unpack as
follows (replacing angle-bracketed names adequately for your case):

* `wget <url to the desired GHC build>`
* `tar jxvf <downloaded file name>`

### Installing

* `cd <location of previously uncompressed ghc folder>`
* `./configure`
* `make install`

### Checking installation

Check that GHC is installed with your desired version with:

* `ghc --version`

## cabal-install

### Prerrequisites

* `apt-get install zlib1g-dev`

### Getting

cabal-install can be downloaded from [Hackage](http://hackage.haskell.org/package/cabal-install).
Choose a version (you might want the _latest_). Then download and unpack as follows:

* `wget <url of cabal source package>`
* `tar zxvf <downloaded file name>`

### Installing

First build cabal-install by running the `bootstrap.sh` script.

* `cd <location of previously uncompressed cabal source folder>`
* `sh bootstrap.sh`

This won't add the `cabal` program to your path. You have to manually add `~/.cabal/bin` to your `$PATH`
environment. Suggested way of doing this is by editing `~/.bashrc` and adding the following lines:

    if [ -d ~/.cabal/bin ]; then
       PATH=$PATH:~/.cabal/bin
       export PATH
    fi

### Checking installation

Check that cabal-install is installed with your desired version with:

* `cabal --version`
