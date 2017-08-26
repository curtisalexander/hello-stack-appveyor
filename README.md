# hello-stack-appveyor

**Repo Purpose:** Testing out AppVeyor with Haskell by following [instructions](https://www.snoyman.com/blog/2016/08/appveyor-haskell-windows-ci) provided by Michael Snoyman.


**Ultimate Purpose:** Want to build statically compiled binaries targeting Windows 7 and Windows 10 environments using Haskell.  Most of the tooling would like to build would be simple, script-like binaries.

For instance, would like to have the ability to print `x` rows of a large csv file without having to load the whole file into memory - ala the `head` command from Linux.
