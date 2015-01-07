#Mac OS X Setup for Development for BeanStack Engineers

This document describes how we usually setup the developmer environment on a new Macbook or iMac. We will setup Ruby, Node and Python environments. It is good to have all three of them, because there could be some dependencies between them (think JSON and node).

The document assumes that the Mac development machine is new.

##System Update

Firstly, you need to update the software and operating system of your OS. For that, click on __Apple Icon > Software Update__

##Google Chrome

Download Google Chrome as your browser. Of course you can just use Safari or any of your preferred browser.

##Homebrew

Homebrew is a package manager for Unix and Linux based OS, and that includes the Mac OS X. It makes it so easy to install stuff and libraries on the command line.

####Install
An important dependency before you install Homebrew is that you need to have the __Command Line Tools__ from Xcode. These has compilers that help to build things from source.

However, Xcode weighs something like 2GB, and if you are in a rush to start developing, you can install only the Command Line Tools without Xcode. We do recommend you to just do that, and only install Xcode when it is necessary to do so (doing iOS development).

__Note:__ If you are running OS X 10.9 Mavericks, then you can install the Xcode Command Line Tools directly from the command line with `$ xcode-select --install`, and you won't need to go download the page and questionnaire.

Else, you will have to download the tools from the Apple Developer Website. To do this you need to go to http://developer.apple.com/downloads, and sign in with your Apple ID. There will be tons of questions to be answered, so be prepared for it.

Once you reach the downloads page, search for "Command line tools", and download the latest __Command Line Tools (OS X Mountain Lion) for Xcode__. Open the __.dmg__ fileonce it's done downloading, and double-click on the installer file to launch the installation.

After this, we can finally install Homebrew! Enter the following line (without the `$`), hit __Enter__ and follow the steps on the screen:

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

##Sublime Text

##Vim

##Python

##MySQL

##Node.js

##JSHint

##Ruby and RVM

##LESS

##Heroku

##MongoDB

##Redis

##Project Folder

##Apps


##References

Many of these references were taken and recompiled from Nicholas Henry's [mac-dev-setup](https://github.com/nicolashery/mac-dev-setup). Many thanks to him!
Also, most of these stuff we do here is what we do in BeanStack. To know more about us, visit our [website](http://www.beanstack.sg).