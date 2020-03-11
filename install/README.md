# Enmap Installation

## Installing enmap

To install Enmap in your project, all you need to do is run the following command:

```javascript
npm i enmap@latest
```

This installs enmap which can be used in memory \(as in, doesn't save to the database\), if that's what you need. Otherwise, keep reading!

### Peer Dependencies

For persistence you need to also install `better-sqlite3`, which is necessary for the sqlite database interaction.

### Pre-Requisites

`better-sqlite3` has a specific prerequisite which is needed to build it. How to install these depends on your operating system, so see below for instructions:

{% tabs %}
{% tab title="Windows" %}
On Windows, two things are required to install better-sqlite3. Python 2.7 and the Visual Studio C++ Build Tools. They are required for any module that is _built_ on the system, which includes sqlite.

To install the necessary prerequisites on Windows, the easiest is to simply run the following command, _under an **administrative** command prompt or powershell:_

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
npm i better-sqlite3
```

This will take a few minutes also, as it needs to build the module from source code.

