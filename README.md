# Windows Setup

Survival guide for non-Windows users to make a Windows machine more UNIX-like and thus more bearable.

> The instructions in this repository have been tested with **Windows 10**.

## Contents


<!-- vim-markdown-toc GFM -->

- [Introduction](#introduction)
- [1. Set up Windows](#1-set-up-windows)
  - [1. Install a custom keyboard layout](#1-install-a-custom-keyboard-layout)
  - [2. Install custom key remappings](#2-install-custom-key-remappings)
  - [3. Customise the touchpad](#3-customise-the-touchpad)
  - [4. Customise the taskbar](#4-customise-the-taskbar)
  - [5. Miscellaneous settings](#5-miscellaneous-settings)
  - [6. Install and configure Windows Terminal](#6-install-and-configure-windows-terminal)
  - [7. Install Git for Windows](#7-install-git-for-windows)
  - [8. Install PowerToys](#8-install-powertoys)
    - [1. Color Picker](#1-color-picker)
    - [2. Paste As Plain Text](#2-paste-as-plain-text)
    - [3. Peek](#3-peek)
    - [4. Screen Ruler](#4-screen-ruler)
    - [5. Text Extractor](#5-text-extractor)
  - [9. Set up eduroam](#9-set-up-eduroam)
- [2. Set up WSL](#2-set-up-wsl)
  - [1. Enable WSL](#1-enable-wsl)
  - [2. Install a Linux distribution](#2-install-a-linux-distribution)
  - [3. Configure WSL](#3-configure-wsl)
  - [4. Set up Linux](#4-set-up-linux)
  - [5. Create a Windows Terminal profile](#5-create-a-windows-terminal-profile)
- [Conclusion](#conclusion)

<!-- vim-markdown-toc -->

## Introduction

If you're reading this, you're probably a non-Windows user who involuntarily has to work on a Windows machine (_ugh!_). This repository contains instructions to get out of this miserable situation as quickly as possible and create an environment that is actually usable to you.

This survival guide consists of the following two main parts:

1. **Set up Windows**
1. **Install Linux through WSL**

In the first part, Windows itself is tweaked to get rid of the worst hindrances for someone coming from macOS or Linux. In the second part, a full-fledged Linux distribution is installed on Windows through the [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/).

> This guide uses WSL 2 and not WSL 1, see [documentation](https://learn.microsoft.com/en-us/windows/wsl/compare-versions) to compare the two versions.

Nobody wants to spend more time than necessary on Windows, so let's not lose any time and set up a Linux environment as quickly as possible!

## 1. Set up Windows

> **General note:** several of the following steps are "outsourced" to their own GitHub repositories. That means that you can find the instructions and everything 
you need to perform the step in this other GitHub repository. These occurrences are indicated with links that look something like this: **👉 Find instructions here**.

### 1. Install a custom keyboard layout

There's nothing more annoying than not being able to type the keys you want to. While Windows comes with a large set of pre-installed keyboard layouts, it might not include the specific variation that you're used to. For these cases, here's how to install a custom keyboard layout:

**[👉 Find instructions here](https://github.com/weibeld-personalisation/logitech-swiss-german-keyboard-layout#windows)**

The above instructions centre around the _Logitech Swiss German_ keyboard layout, however, it works in exactly the same way for any other keyboard layout. The only thing you needs is your desired keyboard layout as a `.klc` file.

### 2. Install custom key remappings

If you come from macOS, having to type `Ctrl-C` instead of `Cmd-C` for copying is a major productivity blocker, especially if you have to switch between the two systems. Fortunately, you can remap these keys to make the Windows shortcuts more similar to the macOS shortcuts. Here's how:

**[👉 Find instructions here](https://github.com/weibeld-personalisation/windows-autohotkey-remappings)**

The above remappings are specifically targeted at macOS users. If you come from Linux, feel free to outcomment or adapt any of the mappings.

### 3. Customise the touchpad

The following settings alleviate some inconveniences from a typical Windows touchpad.

In _**Settings > Devices > Touchpad > Taps**_, make the following changes:

1. Set _**Touchpad sensitivity**_ to _**Low sensitivity**_
1. Unselect _**Press the lower right corner of the touchpad to right-click**_
1. Unselect _**Tap twice and drag to multi-select**_

### 4. Customise the taskbar

The following settings make the taskbar more pleasant to look at:

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

Next, some miscellaneous annoyances to get rid of:

1. Disable the [Task View](https://en.wikipedia.org/wiki/Task_View) timeline:
   1. In _**Settings > Privacy > Activity history**_, unselect everything
   1. In _**Settings > System > Multitasking**_, disable _**Timeline**_
1. Disable automatic display brightness adjustment:
   1. In _**Settings > System > Display**_, disable _**Change brightness automatically when lighting changes**_
1. Disable the system beep ("bell") sound:
   1. In _**Settings > System > Sound > Related Settings > Sound Control Panel > Sounds**_, set _**Default Beep > Sounds**_ to _**None**_

### 6. Install and configure Windows Terminal

[Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/) is planned to be Microsoft's [new](https://devblogs.microsoft.com/commandline/introducing-windows-terminal/) de-facto standard terminal application on Windows (replacing the old [Windows Console](https://learn.microsoft.com/en-us/windows/console/)). It is currently not yet included by default on Windows, but it is **highly** recommended and once you have installed it, it will be the only terminal application that you will ever use on Windows.

There are two ways to install Windows Terminal:

1. With the [winget](https://learn.microsoft.com/en-us/windows/package-manager/) package manager
1. From the [Windows Terminal GitHub repository](https://learn.microsoft.com/en-us/windows/package-manager/)

With winget, it's as simple as this:

```powershell
winget install Microsoft.WindowsTerminal
```

To install from GitHub, proceed as follows:

1. Go to the [GitHub releases](https://github.com/microsoft/terminal/releases) page and select the desired release
1. Download the `.msixbundle` file from this release
1. Install it by double-clicking

The drawback of using winget is that you might not get the newest version of Windows Terminal, whereas by installing from GitHub, you can choose the precise version you want.

> Once installed, you can locate Windows Terminal as `wt` in the start menu.

Windows Terminal can be fully configured through a single JSON file called `settings.json`.

Windows Terminal can be customised and configured in a myriad of ways, and it's worth doing so because this is where you will probably spend 90% of your time when you're working on the Windows machine.

The entire configuration is contained in a single JSON file called `settings.json`. That means, customising Windows Terminal is as easy as importing a custom `settings.json` file into Windows Terminal. Here is a ready-to-use `settings.json` file and how to apply it:

**[👉 Find instructions here](https://github.com/weibeld-personalisation/settings-windows-terminal)**

Feel free to adjust the settings file to your needs. You can find all the supported properties and their values in the [Windows Terminal documentation](https://learn.microsoft.com/en-us/windows/terminal/).

### 7. Install Git for Windows

This is not for using Git on Windows (_God forbid!_) but for making it as straightforward as possible to set up Git credentials in the Linux distribution in WSL later.

In particular, the purpose for installing Git on Windows is actually only to have the [Git Credential Manager](https://github.com/git-ecosystem/git-credential-manager) running on Windows, which can then be accessed from Git in the installed Linux instances as their credential manager. This is the [recommended way](https://github.com/weibeld-personalisation/settings-windows-terminal/blob/main/settings.json) of setting up Git credentials for Linux in WSL.

To install Git for Windows, proceed as follows:

1. Go to the [GitHub releases](https://github.com/git-for-windows/git/releases) page of the Git for Windows GitHub repository
1. Select the latest stable release and  download the `*-64-bit.exe` file of this release
1. Install it by double-clicking and accept all the default options of the installer

That's it! You never need to use Git itself on Windows.

### 8. Install PowerToys

[Microsoft PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/) is a set of small utilities that are surprisingly well-made and handy. Some of them provide functionality that you might be used to from macOS and that are lacking from Windows by default. In any case, PowerToys can come in pretty handy on Windows.

PowerToys can be installed with [winget](https://learn.microsoft.com/en-us/windows/package-manager/) as follows:

```powershell
winget install Microsoft.PowerToys --source winget
```

Once installed, you can open the PowerToys GUI which lists all the available utilities in the left sidebar. Some of these utilities are enabled by default and others are disabled.

Below we will focus on the following utilities that either complement macOS behaviour or are otherwise generally useful:

1. [Color Picker](https://learn.microsoft.com/en-us/windows/powertoys/color-picker)
1. [Paste As Plain Text](https://learn.microsoft.com/en-us/windows/powertoys/paste-as-plain-text)
1. [Peek](https://learn.microsoft.com/en-us/windows/powertoys/peek)
1. [Screen Ruler](https://learn.microsoft.com/en-us/windows/powertoys/screen-ruler)
1. [Text Extractor](https://learn.microsoft.com/en-us/windows/powertoys/text-extractor)

#### 1. Color Picker

This is similar to the [Digital Color Meter](https://support.apple.com/en-gb/guide/digital-color-meter/welcome/mac) utility on macOS.

If the default activation shortcut conflicts with any of the [custom key remappings](#2-install-custom-key-remappings) above, set it to something like `Alt-C`. Now you can press `Alt-C` in any situation to open the colour picker.

#### 2. Paste As Plain Text

This is similar to the built-in `Cmd-Opt-Shift-V` shortcut on macOS that allows pasting text as plain text even if it includes formatting information.

If the default activation key conflicts with any of the [custom key remappings](#2-install-custom-key-remappings) above, set it to something else like `Alt-V`. Now, if a text paste introduces unnecessary formatting, just paste it again with `Alt-V` to get nothing but the plain text.

#### 3. Peek

This is similar to the [Quick Look](https://en.wikipedia.org/wiki/Quick_Look) feature of macOS that shows a preview of a selected file when pressing `Space`.

PowerToys doesn't allow to define a `Space` as an activation shortcut, however, you can set it to something similar like, for example, `Win-Space`.

#### 4. Screen Ruler

This allows measuring pixels on the screen in various useful ways which can be useful in many circumstances.

The default activation shortcut of `Win-Shift-M` seems to work fine for this utility.

#### 5. Text Extractor

This is probably the most remarkable utility as it allows performing optical character recognition (OCR) on any part of the screen. This can be very useful for situations like extracting text from a video conference presentation.

After selecting a rectangle on the screen, the extracted text is saved immediately in the clipboard and is ready to be pasted. The default activation shortcut of `Win-Shift-T` seems to work fine for this utility.

### 9. Set up eduroam

Finally, if you have access to [eduroam](https://eduroam.org/), here's how to set it up on Windows:

**[👉 Find instructions here](https://github.com/weibeld-personalisation/eduroam)**

## 2. Set up WSL

Now that Windows itself has been tamed a little bit, it's time to install Linux so that you can spend 90% of your time in a Linux environment and partly forget that you're actually working on a Windows machine.

The traditional way of running Linux on Windows has been to either use [dual boot](https://en.wikipedia.org/wiki/Multi-booting) or run Linux as a virtual machine (VM) on Windows. However, Microsoft provides a more performant and native way to run Linux called [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/).

> There exists [WSL 1 and WSL 2](https://learn.microsoft.com/en-us/windows/wsl/compare-versions) which use different underlying technologies. This guide focuses exclusively on WSL 2 and all mentions of "WSL" assume WSL 2.

WSL is essentially a type 1 (i.e. bare-metal) hypervisor built into Windows (specifically, the [Hyper-V](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/) hypervisor from Microsoft is used). Linux distributions then run like VMs on this hypervisor.

However, what differentiates WSL from just running Linux in VMs is the performance and tight integration with the Windows host system. WSL Linux distributions install and launch very quickly and runtime performance is usually very good because [WSL uses fewer resources than VMs](https://learn.microsoft.com/en-us/windows/wsl/faq#why-would-i-use-wsl-rather-than-linux-in-a-vm-). Additionally, all files on the Windows host system can be seamlessly accessed from Linux (and vice versa) and Windows executables can be executed from Linux as well.

Let's get started with setting up WSL!

### 1. Enable WSL

WSL is included by default in Windows and it just needs to be enabled. To do so, run the following **as an administrator** in a Windows shell:

```powershell
wsl --install
```

To open a shell as an administrator, you can locate Windows Terminal in the start menu (search for `wt`) and then click on _**Run as administrator**_.

When the installation completes, close Windows Terminal and reopen it in order to be back in a non-admin shell.

### 2. Install a Linux distribution

The next step is to install a Linux distribution in WSL, which can be done with the following simple command:

```powershell
wsl --install <Distribution>
```

Where `<Distribution>` is the name of the Linux distribution to install.

To list all the distributions available to you, you can run the following command:

```powershell
wsl -l -o
```

> Note that for this guide, a Debian-based Linux distribution, such as **Ubuntu**, **Debian**, or **Kali Linux** is preferred. This is because the Linux setup further down in this guide is restricted to Debian-based Linux systems.

During the installation, you will be asked for a username and password for the default Linux user that will be created. When the installation completes, you're dropped in a Linux shell in your new full-fledged Linux distribution.

_Hooray!_

The `wsl` command is your tool to manage your Linux distributions in WSL. Here are some of the most important commands:

```powershell
# Start a specific Linux distribution
wsl -d <Distribution>
# Terminate a specific Linux distribution
wsl -t <Distribution>
# Terminate all Linux distributions
wsl --shutdown
# List information about all installed Linux distributions
wsl -l -v
# Uninstall a specific Linux distribution
wsl --unregister <Distribution>
```

These commands are best executed in a Windows shell, such as PowerShell or Command Prompt. However, you can also run the `wsl` command from Linux (as mentioned, you can run Windows executables from Linux in WSL), but in that case, you _must_ append the `.exe` extension, so the command that you have to use from Linux would be `wsl.exe`.

> You can find the complete documentation of the `wsl` command in the [WSL documentation](https://learn.microsoft.com/en-us/windows/wsl/basic-commands).

### 3. Configure WSL

WSL has mainly [two configuration files](https://learn.microsoft.com/en-us/windows/wsl/wsl-config) named `.wslconfig` and `wsl.conf`:

- [`.wslconfig`](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#wslconfig) is located in your home directory on **Windows**
  - Contains settings applying to all Linux distributions
- [`wsl.conf`](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#wslconf) is located in `/etc` in every **Linux distribution**
  - Contains settings applying to a specific Linux distribution

You can find the available settings that can be put in each configuration file in the documentation for [`.wslconfig`](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configuration-setting-for-wslconfig) and [`wsl.conf`](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#configuration-settings-for-wslconf), respectively.

For now, we need to put only a single setting into `wsl.conf` in our Linux distribution. To do so, execute the following command from within the Linux distribution:

```
cat <<EOF | sudo /etc/wsl.conf >/dev/null
[boot]
systemd = true
EOF
```

The above command creates the `/etc/wsl.conf` file with a setting that enables systemd as the Linux distribution's init system (see [documentation](https://learn.microsoft.com/en-us/windows/wsl/wsl-config#systemd-support)). Using systemd is recommended for all Linux distributions and it's also required to make, for example, Docker run out-of-the-box.

After creating or editing the `/etc/wsl.conf` file, it's important to terminate and restart the Linux distribution in order for the settings to be applied. As mentioned above, you can do this from a Windows shell as follows:

```powershell
wsl -t <Distribution>
wsl -d <Distribution>
```

Once you're back in the Linux distribution, you can verify that systemd is indeed running:

```bash
sudo systemctl status
```

### 4. Set up Linux

The next step is to set up Linux with the customisations, settings, and tools that you're used to so that you will feel right at home. Below is a script that performs this setup in one go in an interactive way:

**[👉 Find instructions here](https://github.com/weibeld-personalisation/linux)**

The above script naturally includes an opinionated set of customisations, settings, and tools. If your needs are different, feel free to adjust it accordingly.

### 5. Create a Windows Terminal profile

So far you probably started your Linux distribution by first launching PowerShell or Command Prompt in Windows Terminal and then running `wsl -d <Distribution>`. This works, however, there is a better way, namely by creating a Windows Terminal _profile_ for your Linux distribution.

A profile includes a command to run at startup and related settings so that when you open this profile, you're dropped right into a specific environment, such as your Linux distribution. You can also set one profile as the default profile so that when you open Windows Terminal, you're automatically dropped into this profile.

To create a new profile for your Linux distribution and set it as the default, proceed as follows:

1. In Windows Terminal type `Ctrl-,` to open the settings
1. In the left settings pane, click on _**Add a new profile > New empty profile**_
1. Configure the following parameters of the new profile:
   1. Set _**Name**_ an arbitrary name for the profile (e.g. "Ubuntu")
   1. Set _**Command line**_ to: `wsl -d <Distribution>`
   1. Set _**Icon**_ to a local image file (find some example icons [here](https://github.com/weibeld-personalisation/settings-windows-terminal/tree/main/icons))
1. Set the created profile as the default profile:
   1. Go to _**Startup**_ in the left settings pane
   1. Set _**Default profile**_ to the profile you just created
1. Click _**Save**_ in the lower right corner of the settings window

Once this is done, quit Windows Terminal and restart it: you should now be dropped right into your Linux distribution.

> Note: the [Windows Terminal settings](https://github.com/weibeld-personalisation/settings-windows-terminal) installed above already include profiles for the Ubuntu and Debian distributions in WSL. If you also installed Ubuntu or Debian, you may either use these existing profiles instead of creating a new one, or you may delete these profiles and create a fresh one.

## Conclusion

Congratulations, by now you should have a setup and workflow that lets you evade the Windows world as swiftly and painlessly as possible:

1. Start up the Windows machine
1. Take a coffee break until the Windows initialisation completes
1. Launch Windows Terminal

And, _boom!_, you're on solid UNIX grounds and can, at least briefly, forget that you're forced to work on a Windows machine! 🎉
