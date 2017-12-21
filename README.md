# Mac OS X Dev Setup

This document describes how I set up my developer environment on a new MacBook or iMac. We will set up [Node](http://nodejs.org/) (JavaScript), [Python](http://www.python.org/), and [Ruby](http://www.ruby-lang.org/) environments, mainly for JavaScript and Python development. Even if you don't program in all three, it is good to have them as many command-line tools use one of them. As you read  and follow these steps, feel free to send me any feedback or comments you may have.

The document assumes you are new to Mac. The steps below were tested on **OS X Mountain Lion**.

If you have any comments or suggestions, feel free to give me a shout [on Twitter](https://twitter.com/nicolahery)!

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Google Chrome](#google-chrome)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Consolas](#consolas)
- [Beautiful terminal](#beautiful-terminal)
- [iTerm2](#iterm2)
- [Git](#git)
- [Sublime Text](#sublime-text)
- [Vim](#vim)
- [code folder](#projects-folder)
- [Apps](#apps)

## System update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > Software Update...**

## System preferences

If this is a new computer, there are a couple tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock

## Google Chrome

Install your favorite browser, mine happens to be Chrome.

Download from [www.google.com/chrome](https://www.google.com/intl/en/chrome/browser/). Open the **.dmg** file once it's done downloading (this will mount the disk image), and drag and drop the **Google Chrome** app into the Applications folder (on the Mac, most applications are installed this way). When done, you can unmount the disk in Finder (the small "eject" icon next to the disk under **Devices**).

## iTerm2

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/) (the newest version, even if it says "beta release").

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it to your first name for example. Then, select **Other Actions... > Set as Default**. Finally, under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.

## Homebrew

Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for OS X is [Homebrew](http://brew.sh/).

### Install

An important dependency before Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source.

Now, Xcode weights something like 2GB, and you don't need it unless you're developing iPhone or Mac apps. Good news is Apple provides a way to install only the Command Line Tools, without Xcode. To do this you need to go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID (the same one you use for iTunes and app purchases). Unfortunately, you're greeted by a rather annoying questionnaire. All questions are required, so feel free to answer at random.

Once you reach the downloads page, search for "command line tools", and download the latest **Command Line Tools (OS X Mountain Lion) for Xcode**. Open the **.dmg** file once it's done downloading, and double-click on the **.mpkg** installer to launch the installation. When it's done, you can unmount the disk in Finder.

**Note**: If you are running **OS X 10.9 Mavericks**, then you can install the Xcode Command Line Tools directly from the command line with `$ xcode-select --install`, and you don't have to go through the download page and the questionnaire.

Finally, we can install Hombrew! In the terminal paste the following line (without the `$`), hit **Enter**, and follow the steps on the screen:

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Open a new terminal tab with **Cmd+T** (you should also close the old one), then run the following command to make sure everything works:

    $ brew doctor
    
### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>
        
To update Homebrew's directory of formulae, run:

    $ brew update
    
**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated
    
To update a package:

    $ brew upgrade <formula>
        
Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

## Consolas

I really like the Consolas font for coding. Being a Microsoft (!) font, it is not installed by default. Since we're going to be looking at a lot of terminal output and code, let's install it now.

There are two ways we can install it. If you bought **Microsoft Office for Mac**, install that and Consolas will be installed as well.

If you don't have Office, follow these steps:

    $ brew install cabextract
    $ cd ~/Downloads
    $ mkdir consolas
    $ cd consolas
    $ curl -O http://download.microsoft.com/download/f/5/a/f5a3df76-d856-4a61-a6bd-722f52a5be26/PowerPointViewer.exe
    $ cabextract PowerPointViewer.exe
    $ cabextract ppviewer.cab
    $ open CONSOLA*.TTF

And click **Install Font**. Thanks to Alexander Zhuravlev for his [post](http://blog.ikato.com/post/15675823000/how-to-install-consolas-font-on-mac-os-x).

## Beautiful terminal

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. What follows might seem like a lot of work, but trust me, it'll make the development experience so much better.

Let's go ahead and start by changing the font. In **iTerm > Preferences...**, under the tab **Profiles**, section **Text**, change both fonts to **Consolas 13pt**.

Now let's add some color. I'm a big fan of the [Solarized](http://ethanschoonover.com/solarized) color scheme. It is supposed to be scientifically optimal for the eyes. I just find it pretty.

Scroll down the page and download the latest version. Unzip the archive. In it you will find the `iterm2-colors-solarized` folder with a `README.md` file, but I will just walk you through it here:

- In **iTerm2 Preferences**, under **Profiles** and **Colors**, go to **Load Presets... > Import...**, find and open the two **.itermcolors** files we downloaded.
- Go back to **Load Presets...** and select **Solarized Dark** to activate it. Voila!

**Note**: You don't have to do this, but there is one color in the **Solarized Dark** preset I don't agree with, which is *Bright Black*. You'll notice it's too close to *Black*. So I change it to be the same as *Bright Yellow*, i.e. **R 83 G 104 B 112**.

Not a lot of colors yet. We need to tweak a little bit our Unix user's profile for that. This is done (on OS X and Linux), in the `~/.bash_profile` text file (`~` stands for the user's home directory).

We'll come back to the details of that later, but for now, just download the files [.bash_profile](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile), [.bash_prompt](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt), [.aliases](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases) attached to this document into your home directory (`.bash_profile` is the one that gets loaded, I've set it up to call the others):

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases
    
With that, open a new terminal tab (Cmd+T) and see the change! Try the list commands: `ls`, `ls -lh` (aliased to `ll`), `ls -lha` (aliased to `la`).

At this point you can also change your computer's name, which shows up in this terminal prompt. If you want to do so, go to **System Preferences** > **Sharing**. For example, I changed mine from "Nicolas's MacBook Air" to just "MacBook Air", so it shows up as `MacBook-Air` in the terminal.

Now we have a terminal we can work with!

(Thanks to Mathias Bynens for his awesome [dotfiles](https://github.com/mathiasbynens/dotfiles).)

## Git

What's a developer without [Git](http://git-scm.com/)? To install, simply run:

    $ brew install git
    
When done, to test that it installed fine you can run:

    $ git --version
    
And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain
    
**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/nicolashery/mac-dev-setup/blob/master/.gitignore) file for inspiration.
    
## Sublime Text

With the terminal, the text editor is a developer's most important tool. Everyone has their preferences, but unless you're a hardcore [Vim](http://en.wikipedia.org/wiki/Vim_(text_editor)) user, a lot of people are going to tell you that [Sublime Text](http://www.sublimetext.com/) is currently the best one out there.

Go ahead and [download](http://www.sublimetext.com/) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shortcut on the OS X Dock for both for Sublime Text and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

Sublime Text is not free, but I think it has an unlimited "evaluation period". Anyhow, we're going to be using it so much that even the seemingly expensive $70 price tag is worth every penny. If you can afford it, I suggest you [support](http://www.sublimetext.com/buy) this awesome tool. :)

Just like the terminal, let's configure our editor a little. Go to **Sublime Text 3 > Preferences > Settings - User** and paste the following in the file that just opened:

```json
{
    "font_face": "Consolas",
    "font_size": 13,
    "rulers":
    [
        79
    ],
    "highlight_line": true,
    "bold_folder_labels": true,
    "highlight_modified_tabs": true,
    "tab_size": 2,
    "translate_tabs_to_spaces": true,
    "word_wrap": false,
    "indent_to_bracket": true
}
```
    
Feel free to tweak these to your preference. When done, save the file and close it.

I use tab size 2 for everything except Python and Markdown files, where I use tab size 4. If you have a Python and Markdown file handy (or create dummy ones with `$ touch dummy.py`), for each one, open it and go to **Sublime Text 3 > Preferences > Settings - More > Syntax Specific - User** to paste in:

```json
{
    "tab_size": 4
}
```

Now for the color. I'm going to change two things: the **Theme** (which is how the tabs, the file explorer on the left, etc. look) and the **Color Scheme** (the colors of the code). Again, feel free to pick different ones, or stick with the default.

A popular Theme is the [Soda Theme](https://github.com/buymeasoda/soda-theme). To install it, run:

    $ cd ~/Library/Application\ Support/Sublime\ Text\ 2/Packages/
    $ git clone https://github.com/buymeasoda/soda-theme/ "Theme - Soda"
    
Then go to **Sublime Text 3 > Preferences > Settings - User** and add the following two lines:

    "theme": "Soda Dark.sublime-theme",
    "soda_classic_tabs": true

Restart Sublime Text for all changes to take effect (Note: on the Mac, closing all windows doesn't close the application, you need to hit **Cmd+Q**).

The Soda Theme page also offers some [extra color schemes](https://github.com/buymeasoda/soda-theme#syntax-highlighting-colour-schemes) you can download and try. But to be consistent with my terminal, I like to use the **Solarized** Color Scheme, which already ships with Sublime Text. To use it, just go to **Sublime Text 3 > Preferences > Color Scheme > Solarized (Dark)**. Again, this is really according to personal flavors, so pick what you want.

Let's create a shortcut so we can launch Sublime Text from the command-line:

    $ sudo ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl;

Now I can open a file with `$ subl myfile.py` or start a new project in the current directory with `$ subl .`. Pretty cool.

Finally, let's enable vim keyboard shortcuts in sublime. Go to **Sublime Text 3 > Preferences > Settings > User** and add the following line:

    "ignore_packages": []

Sublime Text is very extensible. For now we'll leave it like that, we already have a solid installation. To add more in the future, a good place to start would be to install the [Sublime Package Control](http://wbond.net/sublime_packages/package_control/installation).

## Vim

Although Sublime Text will be our main editor, it is a good idea to learn some very basic usage of [Vim](http://www.vim.org/). It is a very popular text editor inside the terminal, and is usually pre-installed on any Unix system.

For example, when you run a Git commit, it will open Vim to allow you to type the commit message.

I suggest you read a tutorial on Vim. Grasping the concept of the two "modes" of the editor, **Insert** (by pressing `i`) and **Normal** (by pressing `Esc` to exit Insert mode), will be the part that feels most unnatural. After that it's just remembering a few important keys.

Vim's default settings aren't great, and you could spend a lot of time tweaking your configuration (the `.vimrc` file). But if you're like me and just use Vim occasionally, you'll be happy to know that [Tim Pope](https://github.com/tpope) has put together some sensible defaults to quickly get started.

First, install [pathogen.vim](https://github.com/tpope/vim-pathogen) by running:

    $ mkdir -p ~/.vim/autoload ~/.vim/bundle && \
        curl -LSso ~/.vim/autoload/pathogen.vim https://tpo.pe/pathogen.vim

Then create a file `~/.vimrc` (you can use `$ subl ~/.vimrc`), and paste in the following:

    execute pathogen#infect()
    syntax on
    filetype plugin indent on

And finally, install the Vim "sensible defaults" by running:

    $ cd ~/.vim/bundle
    $ git clone git://github.com/tpope/vim-sensible.git

With that, Vim will look a lot better next time you open it!

## python

We'll install python3 using pyenv.

First, uninstall everything.

    $ brew uninstall python3
    $ brew uninstall python

Ensure which python3 is empty, and which python is /usr/bin/python and is a Python 2 (it comes with OS X). Nuke any system-wide pip pacakges:

    $ pip freeze | sudo -H xargs pip uninstall -y

Install pyenv

    $ brew install pyenv pyenv-virtualenv

Add these lines to ~/.bash_profile:

    $ if which pyenv > /dev/null; then eval "$(pyenv init -)"; fi
    $ if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi

Open a new shell and install python 3.6.1:

    $ env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install -v 3.6.1
    $ pyenv global 3.6.1

## code folder

This really depends on how you want to organize your files, but I like to put all my version-controlled projects in `~/code`. Other documents I may have, or things not yet under version control, I like to put in `~/Documents` which I back up to google drive.

## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [Google Drive](https://www.google.com/drive/download/): File syncing to the cloud. I automatically back up ~/Documents and ~/Photos. 
- [Spectacle Window Manager](s) allows you to easily move windows around with keyboard shortcuts.



