---
description: >-
  To install Enmap, please read these instructions very carefully, every word is
  important!
---

# Enmap Installation

Enmap is a wrapper around better-sqlite3, which requires to be built directly on your system. As such, you need to install pre-requisites first. Please follow these instructions _to the letter_. If it's not written here, you probably shouldn't do it unless you know _why_ you're doing it.

## Pre-Requisites

{% hint style="warning" %}
SQLite modules usually only successfully work on LTS versions of node. This means it will work correctly on node 12, and 14. It will _not_ work on node 13, 15, 17. Make sure you have the right version, check this with `node -v`.

Also, better-sqlite3 doesn't compile on unreleased node versions usually. Your mileage may vary, but don't expect it to work on the "Latest" version of node either.
{% endhint %}

How to install the pre-requisites depends on your operating system, so see below for instructions:

{% tabs %}
{% tab title="Windows" %}
On Windows, two things are required to install better-sqlite3. Python, and the Visual Studio C++ Build Tools. They are required for any module that is _built_ on the system, which includes sqlite.

To install the necessary prerequisites on Windows, the easiest is to simply run the following commands separately, _under an **administrative** command prompt or powershell:_

```javascript
// First run:
npm i -g --add-python-to-path --vs2015 --production windows-build-tools

// Then run:
npm i -g node-gyp@latest
```

> It's _very important_ that this be run in the **administrative** prompt, and not a regular one.

Once the windows-build-tools are installed \(this might take quite some time, depending on your internet connection\), **close all open command prompts, powershell windows, and editors with a built-in console/prompt**. Otherwise, the next command will not work.
{% endtab %}

{% tab title="Linux" %}
On Linux, the pre-requisites are much simpler in a way. A lot of modern systems \(such as Ubuntu, since 16.04\) already come with python 2.7 pre-installed. For some other systems, you might have to fiddle with it to either get python 2.7 installed, or to install both 2.7 and 3.x simultaneously. Google will be your friend.

As for the C++ build tools, that's installed using the simple command: `sudo apt-get install build-essential` for most debian-based systems. For others, look towards your package manager and specificall "GCC build tools". Your mileage may vary but hey, you're using Linux, you should know this stuff.
{% endtab %}

{% tab title="Mac OS" %}
As of writing this page, MacOS versions seem to all come pre-built with Python 2.7 on the system. You will, however, need the C++ build tools.

* Install [XCode](https://developer.apple.com/xcode/download/)
* Once XCode is installed, go to **Preferences**, **Downloads**, and install the **Command Line Tools**.

Once installed, you're ready to continue.
{% endtab %}
{% endtabs %}

## Installing Enmap

Once those pre-requisites are installed \(if they're not, scroll up, and _follow the instructions_\), and you've closed all open command prompts, open a new, _normal_ \(not-admin\) command prompt or terminal in your project, then install Enmap using the following command:

```text
npm i enmap
```

This will take a few minutes, as it needs to build better-sqlite3 from source code, and then install enmap itself.  Note that "a few minutes" can be 1 or 30 minutes, it really depends on your hardware and configuration.

If you get any errors, please see the [Troubleshooting Guide](troubleshooting-guide.md). If the guide doesn't help, join the Discord \(link at the top of this page\).

