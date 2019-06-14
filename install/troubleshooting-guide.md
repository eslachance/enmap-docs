---
description: '"Anything that can go wrong will go wrong" - Murphy''s Law'
---

# Troubleshooting Guide

## MSB3428: Could not load the Visual C++ component "VCBuild.exe"

[Looks like someone hasn't follows the installation instructions correctly...](./#pre-requisites)

## Error: Command failed: C:\some-python3x-path\python.EXE

node-gyp \(used to build better-sqlite3\) is not compatible with Python 3. Yes, it's been 10 years since 3's release. Yes, it sucks. But you need to have python 2.7.x in your path to install better-sqlite3. If you're not using python anywhere else, uninstall it and make sure to [follow my installation instructions](./#pre-requisites). If you are, run `npm config set python python2.7` before running the install again.



