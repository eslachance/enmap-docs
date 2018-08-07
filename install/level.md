# Enmap-Level

## Pre-Requisites

The `enmap-level` provider is the fastest one in terms of pure performance, but it has one serious limitation: it can only be opened from one location, which means it is incompatible with any sharding/clustering/multi-process system. Beyond the performance advantage, since it's file-based, it does not require the installation of any additional server software for the database to be used.

{% tabs %}
{% tab title="Windows" %}
On Windows, two things are required to install enmap-sqlite. Python 2.7 and the Visual Studio C++ Build Tools. They are required for any module that is _built_ on the system, which includes sqlite. 

> The Windows Built Tools require over 3GB of space to install and use. Make sure you have enough space before starting this download and install!

To install the necessary pre-requisites on Windows, the easiest is to simply run the following command, _under an **administrative** command prompt or powershell:_

```javascript
npm i -g --production windows-build-tools
```

> It's _very important_ that this be run in the **administrative** prompt, and not a regular one.

Once the windows-build-tools are installed \(this might take quite some time, depending on your internet connection\), close all open command prompts, powershell windows, and editors with a built-in console/prompt. Otherwise, the next command will not work. 
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

## Installing enmap-level

Once the pre-requisites are installed, the following command _should_ install `enmap-level`. Simply run this command: 

```text
npm i enmap-level
```

This might take a few minutes so be patient. A lot of things will be shown on the screen, that's normal. Unless the whole process ends in a large block of red text, don't worry about it. 

## Initialization

Enmap-Level doesn't have many options since it's a simple file-based system. The default lines required to work with `enmap` and `enmap-level` are: 

```javascript
// Load Enmap
const Enmap = require('enmap');
 
// Load the Provider
const Provider = require('enmap-level');
 
// Initialize the provider
const provider = new Provider({ name: 'test' });
 
// Initialize the Enmap with the provider instance.
const myEnmap = new Enmap({ provider });
```

The only option available for the provider beyond the name, is the path. You can store enmap-level data anywhere, even outside the project's folder, by giving it a relative or absolute folder path on the system. For instance: 

```javascript
// Default data directory
const provider = new Provider({ 
  name: "test",
  dataDir: './data'
});

// Absolute directory

const provider = new Provider({ 
  name: "test",
  dataDir: '/etc/enmap/data'
});

// Relative, one higher than the file it's called from.
const provider = new Provider({ 
  name: "test",
  dataDir: '../enmap-data'
});
```



