# hello-stack-appveyor

[![Build status](https://ci.appveyor.com/api/projects/status/9rp94ob7adhon3ar/branch/master?svg=true)](https://ci.appveyor.com/project/curtisalexander/hello-stack-appveyor/branch/master)

## Purpose

### Beginnings
First, this was setup in order to test out AppVeyor with Haskell by following the [instructions](https://www.snoyman.com/blog/2016/08/appveyor-haskell-windows-ci) provided by Michael Snoyman.

### Eventually
Eventually, I want to build statically compiled binaries targeting Windows 7, Windows 10, macOS, and possibly Linux environments using Haskell.  Most of the tooling I would like to build would be simple, script-like programs that compile to a native binary.

For instance, on Windows I would like to have the ability to print `x` # of rows from a large csv file without having to load the whole file into memory - ala the `head` command from Linux.

And yes, I can use some programming language to stream rows of a csv -- such as using [csvkit](http://csvkit.readthedocs.io/en/latest/) within a Python environment -- but I would like to have a binary that I can distribute to team members who don't have Python setup on their machines.


## Aside - [Scoop](http://scoop.sh) for Windows
Even though many command line tools, such as `head`, already exist for Windows, I may still want to create Haskell versions as a learning exercise.

### `head` on Windows Today
To get the `head` command on Windows, first install [scoop](http://scoop.sh) by running the following from Powershell 3

```
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```

and then installing [coreutils](https://github.com/lukesampson/scoop/blob/master/bucket/coreutils.json) by running the following

```
scoop install coreutils
```

In addition, I would like to utilize `scoop` in order to create [custom buckets](https://github.com/lukesampson/scoop/wiki/Buckets#creating-your-own-bucket) to install and manage the Haskell compiled binaries.


## Single Script, Multiple Native Binaries
My ultimate dream is to have a single script from which I can utilize free CI services to compile binaries that I then can download and install within whatever environment I am working in.  In a way, I'll use this repo as an example to document my progress (which may be a bit slow depending upon my work commitments at the time).

I would like to do something like the following.

* From my macOS machine at home, write a Haskell script (most likely a script that works with data in a [streaming](https://haskell-lang.org/library/conduit) or [concurrent](https://haskell-lang.org/library/async) manner).
    * See also the work written up by Chris Done on [working with data in Haskell](https://www.fpcomplete.com/blog/2016/09/data-haskell).
* Commit the script to Github, which in turn would trigger CI builds on [AppVeyor](https://www.appveyor.com/) and [TravisCI](https://travis-ci.org/).
* I would like for the builds on the CI servers to ultimately compile static binaries of the Haskell scripts I write.
* Then I would have these binaries pushed / saved to `...`
    * As of now, I am unsure where / how to push these binaries.
    * Perhaps I can just push to the [releases](https://github.com/curtisalexander/hello-stack-appveyor/releases) section of the project repo).
    * This is definitely the area I'm most fuzzy as to how I can accomplish.  Will need to review the following AppVeyor docs.
        * [Packaging artifacts](https://www.appveyor.com/docs/packaging-artifacts/)
        * [Publishing artifacts to GitHub releases](https://www.appveyor.com/docs/deployment/github/)
* Finally, I would install the binaries.
    * Windows
        * Create an [app manifest](https://github.com/lukesampson/scoop/wiki/App-Manifests) that points to the newly created binaries.
        * Utilize [scoop](http://scoop.sh) to install the tool on Windows.
    * macOS
        * Utilize [homebrew](https://brew.sh/) to create a [custom tap](https://github.com/Homebrew/brew/blob/master/docs/How-to-Create-and-Maintain-a-Tap.md) and then install.
    * Linux
        * Not sure how to install as there are a variety of package managers and it depends on the environment I would be working on.
        * Might be as simple as a `curl` command to download the binary and place in an appropriate directory on my `$PATH`.
    * [nixOS](https://nixos.org/)
        * How could I use this?
    * [Docker](https://www.docker.com/)
        * How could I use this?
