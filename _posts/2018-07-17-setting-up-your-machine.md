---
layout: post
title: "Setting Up Your Machine"
excerpt_separator: "<!--more-->"
categories:
  - Environment
tags:
  - Setup
  - Environment 
  - NativeScript 
last_modified_at: 2018-07-17T10:30:00-00:00
---

There are many different ways to set up your development environment for NativeScript. Here I'll show you mine.
<!--more-->

The following shows the list I use to set up my machine for NativeScript development on my Mac.

If you are not recovering from a computer crash like me, then you can ignore reformatting your Mac :)

**Note: Replace iTerm2 with your preferred terminal and VSCode with your preferred IDE**

## Optional
* Open Disk Utility and Reformat "Macintosh HD"
* Reinstall Mac OS


## Basics
* Install Chrome
* Install iTerm2
* Open iTerm2
* Create/Import .bash_prompt

    Run `touch .bash_prompt` in iTerm2
* Create/Import .bash_profile

    Run `touch .bash_profile` in iTerm2
* Create/Import .git_completion.sh

    Run `touch .git_completion.sh` in iTerm2
* Create/Import .git_prompt.sh

    Run `touch .git_prompt.sh` in iTerm2
* Install Homebrew

    Run `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` in iTerm2
* Install nvm

    Run `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash` in iTerm2
* Install the latest version of Node via nvm

    Run `nvm install node` in iTerm2
* Install NativeScript CLI

    Run `npm install -g nativescript` in iTerm2
* Install Xcode
* Open Xcode (Accept the prompt to install tools)
* Go to Xcode/Preferences/Locations and Select "Xcode x.x.x" in the Command Line Tools dropdown
* Install Android Studio
* Run the ruby NativeScript setup command in iTerm2

    `ruby -e "$(curl -fsSL https://www.nativescript.org/setup/mac)"`
* Run `tns doctor` in iTerm2
* Follow the prompts and allow it to set up iOS and Android requirements for you
* _Fix any issues found by the doctor_ :) 

**Note: See the Common Issues and Fixes section below for solutions I found that might help you**

* Run `tns doctor` in iTerm2 to see if you fixed all issues
* Open Android Virtual Device Manager and Create an Android emulator
* Start the emulator manually to make sure it was set up correctly
* Install VS Code
* Run `tns create testApp --template tns-template-blank-ng` in iTerm2
* Run `cd testApp` in iTerm2
* Run `cd app` in iTerm2
* Run `tns run ios --emulator` in iTerm2
* Once the iOS simulator loads the app press `ctrl` + `c` in iTerm2
* Run `tns run android` in iTerm2
* Once the Android simulator loads the app press `ctrl` + `c` in iTerm2


If you were able to get the iOS simulator and Android emulator to load the blank template app then you are done.

**Still having issues? Here is what you can do**

* Refer to the NativeScript Documentation on installation
* Google your specific error message, someone likely has seen and fixed your exact error



## Additional Apps
* **f.lux**: Helps reduce eye strain
* **BetterSnapTool**: Makes window management a breeze
* **Tunnelbear**: My preferred VPN client
* **Charles**: Proxy to help debug network calls on mobile device and inside of iOS simulator
* **Spotify**: Music is good for the soul!



## Additional OSX Setup

_Just a few things I like to do as well_

* System Preferences/Accessibility/Keyboard/Keyboard Preferences/Shortcuts Select "All Controls" at the bottom

    Allows you to tab through buttons/options in OSX dialogs
    
* System Preferences/Mission Control uncheck "Automatically rearrange Spaces based on most recent use"

    Spaces are the key to my productivity on a Mac, it's important my Spaces don't get moved around on me!

* System Preferences/Displays Uncheck "Automatically Adjust Brightness"

    I find this annoying

* System Preferences/Energy Saver Increase threshold for turning off display

    I also find this annoying
    
* System Preferences/Trackpad uncheck "Force Click and haptic feedback"

    I'm just not a fan of the Force Click..



## Common Issues and Fixes

* Missing/Unable to find ANDROID_HOME variable

     To fix run `export ANDROID_HOME=/Users/$(whoami)/Library/Android/sdk` in iTerm2`
    
* Missing Android SDK version 23<= and >=27

    1. Open Android Studio
    2. Open SDK Manager
    3. Check the checkbox next to a version between 23 and 27.
    4. Click Accept/Install




If you run into any issues I didn't, stop by the [NativeScript Setup Docs](http://docs.nativescript.org/start/quick-setup "NativeScript Setup Link") for a more in depth setup guide.
