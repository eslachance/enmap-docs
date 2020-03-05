# Enmap Installation

## Installing enmap

{% hint style="warning" %}
In order to install Enmap, you'll need a few things installed on your machine. First off, you need NodeJS \(Node 10 is required. Not 8, not 9, not 12. _**NODE 10 ONLY**_\). For Windows and MacOS, simply[ download and install from the website](https://nodejs.org/en/download/). For Linux, see [this page for installation](https://nodejs.org/en/download/package-manager/).
{% endhint %}

To install Enmap in your project, all you need to do is run the following command:

```javascript
npm i enmap@latest
```

This may take a few minutes, then you're ready to use it.

### Peer Dependencies

For persistence you need to also install `better-sqlite-pool`, which is necessary for the sqlite database interaction.

### Pre-Requisites

`better-sqlite-pool` has a specific pre-requisite which is needed to build it. How to install these depends on your operating system, so see below for instructions:

{% tabs %}
{% tab title="Windows" %}
On Windows, two things are required to install enmap-sqlite. Python 2.7 and the Visual Studio C++ Build Tools. They are required for any module that is _built_ on the system, which includes sqlite.

> The Windows Build Tools require over 3GB of space to install and use. Make sure you have enough space before starting this download and install!

To install the necessary pre-requisites on Windows, the easiest is to simply run the following command, _under an **administrative** command prompt or powershell:_

```javascript
npm i -g --add-python-to-path --vs2015 --production windows-build-tools
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

Once those pre-requisites are installed, simply run the following command:

```text
npm i better-sqlite-pool
```

This will take a few minutes also, as it needs to build the module from source code.

