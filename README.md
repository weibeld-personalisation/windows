# Windows Setup

Step-by-step guide for making a Windows machine more macOS/Linux-like as quick as possible.

> The instructions in this repository have been tested with **Windows 10**.

## Contents


<!-- vim-markdown-toc GFM -->

- [Introduction](#introduction)
- [Configure Windows](#configure-windows)
  - [1. Install a custom keyboard layout](#1-install-a-custom-keyboard-layout)
  - [2. Install custom key remappings](#2-install-custom-key-remappings)
  - [3. Customise the touchpad](#3-customise-the-touchpad)
  - [4. Customise the taskbar](#4-customise-the-taskbar)
  - [5. Miscellaneous settings](#5-miscellaneous-settings)
  - [6. Install and configure Windows Terminal](#6-install-and-configure-windows-terminal)
    - [Installation](#installation)
    - [Configuration](#configuration)
  - [7. Install Git for Windows](#7-install-git-for-windows)
  - [8. Install and configure PowerToys](#8-install-and-configure-powertoys)
    - [Color Picker](#color-picker)
    - [Paste As Plain Text](#paste-as-plain-text)
    - [Peek](#peek)
    - [Screen Ruler](#screen-ruler)
    - [Text Extractor](#text-extractor)
  - [9. Set up eduroam](#9-set-up-eduroam)
- [Configure WSL](#configure-wsl)
  - [1. Enable WSL](#1-enable-wsl)
  - [2. Install a Linux distribution in WSL](#2-install-a-linux-distribution-in-wsl)
  - [3. Configure WSL settings for the Linux distribution](#3-configure-wsl-settings-for-the-linux-distribution)
  - [4. Configure the Linux distribution](#4-configure-the-linux-distribution)
  - [5. Create a Windows Terminal profile for the Linux distribution](#5-create-a-windows-terminal-profile-for-the-linux-distribution)

<!-- vim-markdown-toc -->

## Introduction

If you're reading this, you're probably a non-Windows user who is forced, through whatever circumstances, to work on a Windows machine (_ugh!_). This repository contains instructions to get out of the hell as quick as possible and create an environment that resembles macOS/Linux as much as possible.

The survival guide consists mainly of the following parts:

1. Configure Windows
1. Install Linux on Windows with [WSL](https://learn.microsoft.com/en-us/windows/wsl/)

Let's bite the bullet and go through it!

## Configure Windows

> The following instructions are sorted by urgency, that is, the most insufferable things are fixed first and the more tolerable things are addressed later. So, it's best to follow the guide in this order.

### 1. Install a custom keyboard layout

> This step is optional if you're not content with any of the included keyboard layouts of Windows.

**To install a custom keyboard layout, follow the instructions [👉 here](https://github.com/weibeld/logitech-swiss-german-keyboard-layout#windows).**

The above instructions are for an example keyboard layout (Logitech Swiss German), however, it works the same for any keyboard layout. All you need for it is your desired keyboard layout as a `.klc` file.

### 2. Install custom key remappings

**To install a set of custom key remappings, follow the instructions [👉 here](https://github.com/weibeld/autohotkey-windows-key-remappings).**

The remappings in the above instructions make the Windows keyboard more similar to a macOS keyboard (for example, use _Win-C_ instead of _Ctrl-C_ for copying, thus resembling _Cmd-C_ on macOS). They also swap the _Caps Lock_ and _Ctrl_ keys, a common customisation among macOS/Linux users to make the _Ctrl_ easier to press.

> Note: the key remappings are independent of the used keyboard layout.

### 3. Customise the touchpad

In _**Settings > Devices > Touchpad > Taps**_, make the following changes:

1. Set _**Touchpad sensitivity**_ to _**Low sensitivity**_
1. Unselect _**Press the lower right corner of the touchpad to right-click**_
1. Unselect _**Tap twice and drag to multi-select**_

### 4. Customise the taskbar

1. In _**Settings > Personalization > Taskbar**_, make the following changes:
   1. Select _**Combine taskbar buttons > Always hide labels**_
   1. Disable _**News and interests > Show news and interests on the taskbar**_
   1. Enable _**Notification area > Select which icons appear on the taskbar > Always show all icons in the notification area**_
   1. Disable all items except _**Clock**_, _**Volume**_, _**Network**_, and _**Power**_ from _**Notification area > Turn system icons on or off**_
1. In _**Settings > Personalization > Start**_, make the following changes:
   1. Disable all items except _**Show app list in Start menu**_
1. Right-click on taskbar and make the following changes:
   1. Enable _**Search > Show search icon**_

### 5. Miscellaneous settings

1. Disable the [Task View](https://en.wikipedia.org/wiki/Task_View) timeline:
   1. In _**Settings > Privacy > Activity history**_, unselect everything
   1. In _**Settings > System > Multitasking**_, disable _**Timeline**_
1. Disable automatic display brightness adjustment:
   1. In _**Settings > System > Display**_, disable _**Change brightness automatically when lighting changes**_
1. Disable the system beep ("bell") sound:
   1. In _**Settings > System > Sound > Related Settings > Sound Control Panel > Sounds**_, set _**Default Beep > Sounds**_ to _**None**_

### 6. Install and configure Windows Terminal

[Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/) is Microsoft's replacement for the old _Windows Console_ that has been traditionally used for running shells like _Command Prompt_ and _PowerShell_. Windows Terminal can run any number of shells (including _Command Prompt_ and _PowerShell_) organised in profiles.

Since Windows Terminal is relatively new (introduced in 2019, see [announcement](https://devblogs.microsoft.com/commandline/introducing-windows-terminal/)), it is not yet included in Windows by default and must be manually installed.

> **After installing Windows Terminal, you can forget about the existence of the built-in _Command Prompt_ and _PowerShell_ applications, you will never need to use them again!**

#### Installation

There are two ways to install Windows Terminal:

- With `winget`:
  ```powershell
  winget install Microsoft.WindowsTerminal
  ```
- From GitHub:
  1. Locate the desired version on https://github.com/microsoft/terminal/releases
  1. Download the `.msixbundle` file from the GitHub release and install it by double-clicking

> You might not get the newest version of Windows Terminal with `winget`, thus, if you want the newest version, install from GitHub.

After installation, open Windows Terminal by typing `wt` into the Windows search box.

#### Configuration

To configure Windows Terminal, apply the custom settings from [👉 here](https://github.com/weibeld/windows-terminal-settings):

1. In Windows Terminal, press _**Shift-Ctrl-Comma**_ to open the settings file
1. Overwrite the content of the settings file with the custom settings in [`settings.json`](https://github.com/weibeld/windows-terminal-settings/blob/main/settings.json)
1. Save the Windows Terminal settings file and restart Windows Terminal

> As mentioned, Windows Terminal is the only terminal application that you will ever need from now on. WSL will run in Windows Terminal, and if you need a _PowerShell_ or _Command Prompt_ shell, you can run them in Windows Terminal too (through their corresponding profiles).

### 7. Install Git for Windows

This is not for using Git on Windows (_God forbid!_) but for making the [Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager) available to the Linux distributions in WSL (that will be installed later). This is the [recommended way](https://github.com/weibeld/windows-terminal-settings/blob/main/settings.json) of setting up Git credentials in WSL.

Install Git for Windows as follows:

1. Locate the latest stable release on https://github.com/git-for-windows/git/releases
1. Download the `*-64-bit.exe` file
1. Install by double-clicking the `.exe` file and accepting all the default options

### 8. Install and configure PowerToys

[Microsoft PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/) is a set of general-purpose utilities and some of them are surprisingly well-made and handy. Let's install and configure the most useful ones of these utilities.

To install PowerToys, run the following in a _PowerShell_ or _Command Prompt_ shell in Windows Terminal:

```powershell
winget install Microsoft.PowerToys --source winget
```

PowerToys has a GUI showing all the utilities in the left sidebar. Some of these utilities are enabled by default and others are disabled.

Below, we will focus on the following utilities which are among the most useful ones:

1. [Color Picker](https://learn.microsoft.com/en-us/windows/powertoys/color-picker)
1. [Paste As Plain Text](https://learn.microsoft.com/en-us/windows/powertoys/paste-as-plain-text)
1. [Peek](https://learn.microsoft.com/en-us/windows/powertoys/peek)
1. [Screen Ruler](https://learn.microsoft.com/en-us/windows/powertoys/screen-ruler)
1. [Text Extractor](https://learn.microsoft.com/en-us/windows/powertoys/text-extractor)

Feel free to also explore the other utilities as there is a lot of useful stuff. Ideally, disable the utilities that you don't use to prevent unwanted triggerings.

> PowerToys launches automatically at startup (you can see this by a PowerToys icon in the notification area of the taskbar). That means, the utilities will always be available without any further actions.

#### Color Picker

This is similar to the [Digital Color Meter](https://support.apple.com/en-gb/guide/digital-color-meter/welcome/mac) utility on macOS.

Change the activation shortcut to something that doesn't conflict with the above key remapping and is easy to press, for example, _Alt-C_. Now you can press _Alt-C_ at any time to open the colour picker.

#### Paste As Plain Text

This allows defining a keyboard shortcut for pasting text as pure plain text even if it has been copied with formatting information. This is **highly** useful, especially when copying text from websites and other documents.

Change the activation shortcut to something that doesn't conflict with the above key remappings, for example, _Alt-V_. Now, if pasting something includes annoying formatting, just paste it again with _Alt-V_ to get only the plain text.

#### Peek

This is similar to the [Quick Look](https://en.wikipedia.org/wiki/Quick_Look) feature of macOS that shows a preview of the file when pressing the _Space_ key on one or more selected files.

In PowerToys, a _Space_ alone can't be used as an activation shortcut, so the best you can do is set it to something similar like _Win-Space_.

#### Screen Ruler

This allows measuring pixels on the screen in various useful ways. I'm not aware of a similar utility on macOS, but in any case it can be very useful, for example, when working with images, building a website, etc.

The default activation shortcut of _Win-Shift-M_ seems to work fine.

#### Text Extractor

This is probably the most remarkable utility as it allows performing optical character recognition (OCR) on any part of the screen. This can be extremely useful, for example, for capturing URLs or other text in a video conference where copy-paste doesn't work.

The default activation shortcut of _Win-Shift-T_ seems to work fine. When selecting a portion of the screen, the extracted text is immediately saved in the clipboard and ready to be pasted with the usual paste key combination.

### 9. Set up eduroam

> This step is optional and applies only if you have [eduroam](https://eduroam.org/) access (linked repo below is private).

**To set up access to eduroam, follow the instructions [👉 here](https://github.com/weibeld/eduroam-setup).**

## Configure WSL

Now that Windows itself is a tiny bit less insufferable, it's time to install Linux on it so that you can forget about 90% of the time that you're actually working on Windows.

One possible way to do this is with the [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/) version 2.

> Alternative ways are running Linux in a virtual machine (VM) or setting up Windows/Linux [dual boot](https://en.wikipedia.org/wiki/Multi-booting).

Note that the following instructions will use Ubuntu as an example Linux distributions, however, the process remains largely the same for other Linux distributions.

### 1. Enable WSL

WSL is included by default in Windows and it just needs to be enabled. This can be done as follows:

1. Open and admin shell, which can be done in either of these ways:
   - Locate Windows Terminal (`wt`) in the start menu and click _Run as administrator_
   - In Windows Terminal, click on the triangle in the tab bar, hold down the _Ctrl_ key and click on either _Command Prompt_ or _PowerShell_
1. In the admin shell, execute the following:
   ```powershell
   wsl --install
   ```
1. When the installation finishes, close and reopen Windows Terminal (in order to be back in a non-admin shell)

### 2. Install a Linux distribution in WSL

The next step is to install a Linux distribution in WSL.

You can list all the available Linux distributions with the following command:

```powershell
wsl -l -o
```

To install a distribution, you can use:

```powershell
wsl --install <Name>
```

Where `<Name>` is the name of the desired distribution, for example `Ubuntu` or `Debian`.

During installation, you will be prompted for a username and password for the Linux user. You can freely choose these credentials.

When the installation completes, you will be dropped in a shell in the installed Linux distribution. You can exit the Linux distribution at any time with `exit`.

From a Windows shell, you can list all installed Linux distributions with:

```powershell
wsl -l -v
```

And you can start a specific distribution with:

```powershell
wsl -d <Name>
````

When you exit a Linux distribution, it keeps running for a few seconds before being terminated. You can always explicitly terminate a Linux distribution with:

```powershell
wsl -t <Name>
```

You can also terminate all running Linux distributions at once with:

```powershell
wsl --shutdown
```

### 3. Configure WSL settings for the Linux distribution

TODO: common settings in `/etc/wsl.conf` that are recommended for all Linux distributions

### 4. Configure the Linux distribution

TODO: create Linux setup script on GitHub and apply it here.

### 5. Create a Windows Terminal profile for the Linux distribution

Since 99% of the time when you open Windows Terminal you want to use a Linux distribution in WSL, it's best to create a corresponding Windows Terminal profile and set it as the default profile. In this way, whenever you open Windows Terminal, you're dropped straight into your Linux distribution.

To do so, proceed as follows:

1. In Windows Terminal type _Ctrl-Comma_ to open the settings
1. In the left settings pane, click on _**Add a new profile > New empty profile**_ and configure the following parameters:
   1. _**Name:**_ any name representing the Linux distribution (e.g. `WSL Ubuntu`)
   1. _**Command line:**_ `wsl -d <Name>`
      - Where `<Name>` is the name of the desired Linux distribution (e.g. `Ubuntu`)
   1. _**Icon**_: any image file representing the Linux distriubtion (check [👉 here](https://github.com/weibeld/windows-terminal-settings/tree/main/icons))
1. In the left settings pane, go to _**Startup**_ and set _**Default profile**_ to the profile you just created
1. Click _**Save**_ in the lower right corner

After that, quit and restart Windows Terminal and you should be dropped right into your Linux distribution.

> It's possible that Windows Terminal has already auto-created a profile for each detected WSL Linux distribution. You may also use this auto-created profile for your Linux distribution, however, if you decide to create a new profile, you can safely delete the auto-created profile.

