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

After Homebrew is installed, we need to ensure that the stuff Homebrew installs are used by the system, rather than the system using the default system libraries. We do this by adding `/usr/local/bin` to the `$PATH` environment variable:

```
$ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile
```

Open a new terminal tab with __Cmd+T__, then run the following command to make sure everything works:

```
$ brew doctor
```

####Usage
To install a package, simply type:

```
$ brew install <formula>
```

To update Homebrew's directory of formulae, run:

```
brew update
```

To update a package:

```
brew upgrade <formula>
```

Homebrew keeps older versions of packages installed. Usually, that will take up some space, and it's good to do some cleanup if you don't need them.

```
brew cleanup
```

To see what versions of formulae you have installed:
```
$ brew list --versions
```

##Git
To install Git, just run
```
$ brew install git
```

When done, to test that Git is installed, you can run:
```
$ git --version
```

And `$ which git` should output `/usr/local/bin/git`.



##Sublime Text

To install, go to http://www.sublimetext.com/2 and download Sublime Text 2.

We will now create a shortcut to launch Sublime Text to open files from the command line:

```
$ cd ~
$ mkdir bin
$ ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" ~/bin/subl
```

Now you can open a file with `$ subl foobar.rb` or start/open a new project in the current directory with `$ subl .`.

I usually use the Monokai Color Scheme for Sublime Text 2, just because it doesn't seem glaring to the eyes. Go to __Sublime Text 2 > Preferences > Color Scheme > Monokai (Bright)__. You can choose any color scheme that suits your taste.

Next install, the [Sublime Package Control](https://packagecontrol.io/installation) for Sublime Text 2. This is a Package Manager for Sublime Text 2 and you can install many plugins for Sublime Text for syntax highlighting, cool stuff for rendering Markdown etc.

##Python

OS X, already ships with Python already installed. But you don't want to mes with the system Python because some tools rely on it, so we will install our version with Homebrew.

```
$ brew install python
```

When done, you will get a summary in the terminal. Running `$ which python` should outut `/usr/local/bin/python`.

The installation of Homebrew's python will also come with Pip, which is a package manager for Python. Now, upgrade both of them:

```
$ pip install --upgrade distribute
$ pip install --upgrade pip
```

Executable scripts from Python packages you install will be put in `/usr/local/share/python`, so let's add it to the $PATH. To do so, we'll create a .path text file in the home directory:

```
$ cd ~
$ subl .path
```

And append these lines to `.path`:
```
PATH=/usr/local/share/python:$PATH
export PATH
```

##MySQL

####Install

WE will install MySQL using Homebrew. To install, run:

```
$ brew update
$ brew install mysql
```

Before we can use MySQL, we first need to set it up:
```
$ unset TMPDIR
$ mkdir /usr/local/var
$ mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp
```

__Note__: `whoami` is a command that will echo your username of OS X.

#### Usage
To start the MySQL server, use the `mysql.server` tool:

```
$ mysql.server start
```

To stop it:
```
$ mysql.server stop
```

You can see the different commands available availab for mysql.server with:
```
$ mysql.server --help
```

To connect with the command-line client, run:
```
$ mysql -uroot
```

(Use `exit` to quit the MySQL shell.)

##Node.js

Install Node.js with Homebrew. If you have problems with installing the JSON gem on RVM, this should help.

```
$ brew update
$ brew install node
```

The formula also installs the npm package manager. However, as suggested by the Homebrew output, we need to add `/usr/local/share/npm/bin` to our path so that npm-installed modules with executables will have them picked up.

To do so, add this line to your ~/.path file, before the export PATH line:

```
PATH=/usr/local/share/npm/bin:$PATH
```

We also need to tell npm where to find the Xcode Command Line Tools, by running:

```
$ sudo xcode-select -switch /usr/bin
```
(If Xcode Command Line Tools were installed by Xcode, try instead:)

```
$ sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer
```

Node modules are installed locally in the node_modules folder of each project by default, but there are at least two that are worth installing globally. Those are CoffeeScript, Grunt and JSHint:

```
$ npm install -g coffee-script
$ npm install -g grunt-cli
$ npm install -g jshint
````

####Npm Usage

To install a package:

```
$ npm install <package> # Install locally
$ npm install -g <package> # Install globally
```

To install a package and save it in your project's package.json file:
```
$ npm install <package> --save
```

To see what's installed:
```
$ npm list # Local
$ npm list -g # Global
```
To find outdated packages (locally or globally):
```
$ npm outdated [-g]
```
To upgrade all or a particular package:
```
$ npm update [<package>]
```
To uninstall a package:
```
$ npm uninstall <package>
```

##Ruby and RVM

#### Install
The best and organised way to install Ruby is to use [RVM](https://rvm.io) (Ruby Version Manager) which allows you to manage multiple versions of Ruby on the same machine. Installing RVM, as well as the latest version of Ruby, is very easy. Just run:

```
$ curl -L https://get.rvm.io | bash -s stable --ruby
```

The following line was also automatically added to your .bash_profile:
```
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```

After that, start a new terminal and run:
```
$ type rvm | head -1
```

You should get the output `rvm is a function`.

####Usage
The following command will show you which versions of Ruby you have installed:

```
$ rvm list
```

The one that was just installed, Ruby 2.0, should be set as default. When managing multiple versions, you switch between them with:
```
$ rvm use system # Switch back to system install (1.8)
$ rvm use 2.0.0 --default # Switch to 2.0.0 and sets it as default
```
Run the following to make sure the version you want is being used (in our case, the just-installed Ruby 1.9.3):
```
$ which ruby
$ ruby --version
```
You can install another version with:
```
$ rvm install 1.9.3
```
To update RVM itself, use:
```
$ rvm get stable
```
RubyGems, the Ruby package manager, was also installed:
```
$ which gem
```
Update to its latest version with:
```
$ gem update --system
```
To install a "gem" (Ruby package), run:
```
$ gem install <gemname>
```
To install without generating the documentation for each gem (faster):
```
$ gem install <gemname> --no-document
```
To see what gems you have installed:
```
$ gem list
```
To check if any installed gems are outdated:
```
$ gem outdated
```
To update all gems or a particular gem:
```
$ gem update [<gemname>]
```
RubyGems keeps old versions of gems, so feel free to do come cleaning after updating:
```
$ gem cleanup
```
To list the gemsets:
```
$ rvm gemset list
```

To change the current gemset:
```
$rvm gemset use <gemsetname>
```
(We usually use a different gemset for different applications so as to achive integrity within local development environments.)

##Heroku
Heroku is a Platform-as-a-Service (PaaS) that makes it easy to deploy your apps online. It supports Ruby on Rails, Django and PHP. We usually use it to stage an application online, and occasionally for production purposes as well.

####Install
Assuming that you have an account (sign up if you don't), let's install the Heroku Client for the command-line. Heroku offers a Mac OS X installer, the Heroku Toolbelt, that includes the client. But for these kind of tools, I prefer using Homebrew. It allows us to keep better track of what we have installed. Luckily for us, Homebrew includes a `heroku-toolbelt` formula:

```
$ brew install heroku-toolbelt
```

Update Heroku:

```
heroku update
```

#### Usage
```
$ heroku login
```

If you don't have a public SSH keyå

##Redis

Redis is a NoSQL database and there are a lot of [cool things](http://oldblog.antirez.com/post/take-advantage-of-redis-adding-it-to-your-stack.html) you can do with it that will be hard with other database solutions. For example, it's often used as session management or cahching by web apps.

##Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [Dropbox](https://www.dropbox.com/)
- [Google Drive](https://drive.google.com/)
- [Evernote](https://evernote.com/)


##References

Many of these references were taken and recompiled from Nicholas Henry's [mac-dev-setup](https://github.com/nicolashery/mac-dev-setup). Many thanks to him!
Also, most of these stuff we do here is what we do in BeanStack. To know more about us, visit our [website](http://www.beanstack.sg).