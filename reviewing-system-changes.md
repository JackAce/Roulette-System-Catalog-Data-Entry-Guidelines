# Reviewing Roulette System Changes

When you commit or merge changes to the dev.jackace.com repository in the `dev` branch, you will kick off a build.

The progress of that build process can be found [here](https://github.com/JackAce/dev.jackace.com/actions).

This performs a number of actions, including re-building the entire web site from scratch, rebuilding all the
web pages, and rebuilding the main JSON file used for the Roulette System Catalog.

This process can take 5 minutes or so, and this happens with every change to the `dev` branch. So if you make
3 changes within the span of 1 minute, it's possible that you may wait 15 minutes or so before seeing the
lates changes.

Once the build is complete AND SUCCESSFUL, you will be able to see your changes here:

[https://dev.jackace.com/gambling/roulette/systems/](https://dev.jackace.com/gambling/roulette/systems/)

If there problems with the build, the build will FAIL and you will continue to see the most recent successful build
of the site.

One major thing that can cause the build to fail would be an invalid JSON file.

