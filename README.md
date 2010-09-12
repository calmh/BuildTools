Nym Networks Build Tools
========================

This repository contains a few scripts that simplify building and maintaing iOS/Xcode projects. Some are more heavily dependent on our coding standards than others.

tag-release
-----------

Creates a new tagged release, by git branching a development branch into a new release preparation branch, increasing build number and setting the new version number, then merging into the release branch.

If your development is on the "develop" branch and your releases are on the "master" branch, you can create a new version "1.0" by:

    tag-release develop master

The new release will be made on the master branched, tagged with a new annotated tag named "v1.0".

build-release
-------------

Build release takes the current source tree and creates a compressed, named and tagged distribution. It contains an iOS "IPA" file and the symbols, archived so you can debug future crash dumps. build-release -h show command options and their default values:

    build-release [options]
     -h               Show help
     -n <name>        Set distribution name           (dev-1.1-85-g3d2d5be)
     -t <target>      Set build target                (iDatacenter)
     -c <conf>        Set build configuration         (Debug Trace)
     -s <sdk>         Set build SDK                   (iphoneos4.1)
     -d <distdir>     Set destination directory       (/Users/jb/Releases)

With no options, this would be a "Debug Trace" configuraiton of the "iDatacenter" target, for the iphoneos4.1 SDK, and archive it in /Users/jb/Releases/iDatacenter-dev-1.1-85-g3d2d5be. All of these values are configurable with their corresponding switches.

uncrustify-all
--------------

This script runs uncrustify (assumed to be available somewhere in the $PATH) on all .m and .h files found under the current directory. Uncrustify is assumed to find it's own configuration file, probably in ~/.uncrustify.cfg. This corrects all of the formatting problems that Xcode is fond of causing in day-to-day work, and should ideally be run before every commit.

The example uncrustify.cfg is my definition of "good coding style" for Objective-C.

changelog
---------

Formats a changelog from the git commit log. Assumes that commits are prefixed with one of either:

- (new): A new feature.
- (chg): A change to an existing feature.
- (fix): A bugfix.
- (dev): A change only relevant to developers - not included in the changelog.
- "Set release version to ([0-9.a-z+])" - Marks the release point.
