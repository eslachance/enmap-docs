---
description: '"Anything that can go wrong will go wrong" - Murphy''s Law'
---

# Troubleshooting Guide

{% hint style="warning" %} Please make sure to read the [install page](https://enmap.evie.dev/install#pre-requisites) **VERY CAREFULLY**! This should solve all the issues you face. If not carry on, but don't say we didn't tell you. {% endhint %}

## It's Taking Suuuuuuuuuuuuuuuuuper Long to Install! Whats up with that?

Your computer has to install some programs and then build everything from source. This is going to take a while depending on your computer speed. Patience is key. We can't speed it up for you. It may look like its frozen but it is not.

## My Question Isn't Awnsered Here! 

Please make sure you read the [install page](https://enmap.evie.dev/install#pre-requisites) first. If you can't find what your looking for you can join the discord [here](https://discord.gg/N7ZKH3P).

## MSB3428: Could not load the Visual C++ component "VCBuild.exe"

[Looks like someone hasn't follows the installation instructions correctly...](./#pre-requisites)

## Error: Command failed: C:\some-python3x-path\python.EXE

node-gyp \(used to build better-sqlite3\) is not compatible with Python 3. Yes, it's been 10 years since 3's release. Yes, it sucks. But you need to have python 2.7.x in your path to install better-sqlite3. If you're not using python anywhere else, uninstall it and make sure to [follow my installation instructions](./#pre-requisites). If you are, run `npm config set python python2.7` before running the install again.
