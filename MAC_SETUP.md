# Setting up a Mac for web development
=====

I've been setting up my environment twice this month, once for my iMac and once for my Macbook Air, my two new weapons of mass creation for my freelance business. I thought I would share it, if ever someone needs it, and more importantly if I have to do this ever again.

Of course this is *my* setup and is for most app just a matter of taste, see it as a kind of todo list and adapt it to your liking.

All software listed are free, unless I write otherwise.

## Not mandatory, still useful.

It's not really specific for web development, but still here is some useful apps I use for a productivity boost. The motto here is "SYNC ALL THE DEVICES", I need to have all my data synched between my two macs and my phone.

* [Google Chrome](http://www.google.com/chrome) : my browser of choice, it's fast and it allows synchronization with a gmail account so that you can keep bookmarks and extension synchronized.
* [SpeedDial 2](https://chrome.google.com/webstore/detail/dgpdioedihjhncjafcpgbbjdpbbkikmi) : this is a chrome extension to have a nice landing page where you can keep your stuff. Much more efficient than bookmark, I'm using it to store links to services, documentations and my project instances. You can also synchronize the links with a speed dial account (*$2 for an unlimited use*).
* [Alfred](http://www.alfredapp.com/) : a sexy app launcher to replace spotlight.
* [Reeder](http://reederapp.com/mac/) : syncs your RSS feeds with google reader and your iDevices (*$10*).
* [Spotify](http://www.spotify.com) : because I feel miserable without music. Again it's synced with my two macs and iPhone (*12€/month for a premium account*).

## Ghost in the shell

Having worked on Linux for more than one year I'm now pretty much dependent of a good command line environment.

* [iTerm 2](http://www.iterm2.com/#/section/home) : an alternative to Mac Os Terminal, try it and adopt it.
* [Homebrew](http://mxcl.github.com/homebrew/) : nice packet manager.
* [Xcode](https://developer.apple.com/technologies/tools/) : I'm using it only because it's a prerequisite to using Homebrew. Once installed you need to add Xcode Command Line Tools in Xcode's preferences.

Once homebrew and Xcode Command Line Tools are installed it might be a good idea to hit `brew doctor` and see if something need to be fixed.


## GIT setup

If you want to install git, you can do it with brew.

`brew install git`

Need some aliases ?

`vi ~/.gitconfig`

And add :

	[alias]
	 	st = status
	 	co = checkout

(I'm not a big user of aliases myself, but you'll find various examples in the Interwebs)

Also don't forget to set a global ignores file :

`git config --global core.excludesfile ~/Workspace/.gitglobalignore`
    
And add :

    # Mac specific
    .DS_Store*
    # PHPStorm project files
    .idea
    # SublimeText project files
	*.sublime-project
	*.sublime-workspace
	# Vagrant files
	Vagrantfile
	
Last but not least, add a nice prompt to your bash shell. Credits to mister [Hubert de Muda](https://github.com/ubermuda/dotfiles/blob/master/.profile) :

`vi ~/.profile`

And paste this : 

	BLACK="\[\033[0;30m\]"    # black
	RED="\[\033[0;31m\]"    # red
	GREEN="\[\033[0;32m\]"    # green
	YELLOW="\[\033[0;33m\]"    # yellow
	BLUE="\[\033[0;34m\]"    # blue
	MAGENTA="\[\033[0;35m\]"    # magenta
	CYAN="\[\033[0;36m\]"    # cyan
	LIGHT_GREY="\[\033[0;37m\]"    # white
	DARK_GREY="\[\033[1;30m\]" # dark grey
	WHITE="\[\033[1;37m\]" # WHITE
	COLOR_OFF="\[\033[0m\]" # OFF
	
	export CLICOLOR="1"
	export PATH="$PATH:/usr/local/mysql/bin/:$HOME/bin"
	export PS1="$RED\$(prompt_last_retval_if_failed)$COLOR_OFF$MAGENTA\$(prompt_path)$YELLOW\$(prompt_git_branch)$COLOR_OFF\$ "
	
	function prompt_last_retval_if_failed {
	    local RET=$?
	    if [ $RET -ne 0 ]; then
	        echo "($RET) "
	    fi
	}
	
	function prompt_path {
	    if [ $HOME = `pwd` ]; then
	        echo '~'
	    else
	        basename `pwd`
	    fi
	}
	
	function prompt_git_branch {
	    branch=`git branch 2> /dev/null | grep -E '^\*' | sed "s/\* //"`
	
	    if [ ! -z "$branch" ]; then
	        if [ "$branch" = "(no branch)" ]; then
	            echo " $branch"
	        else
	            dirty=`git status -s 2> /dev/null`
	
	            if [ ! -z "$dirty" ]; then
	                dirty='*'
	            fi
	            echo " ($branch$dirty)"
	        fi
	    fi
	}
	
	prompt_git_branch
	
	#[[ $- == *i* ]] && . /Users/ash/git/git-prompt/git-prompt.sh
	
	if [ -f `brew --prefix`/etc/bash_completion ]; then
	    . `brew --prefix`/etc/bash_completion
	fi

Now you've got branch name and dirty state right in your prompt, plus the return code if something went wrong !

## Install a PHP 5.4 environment with Vagrant

Although you can absolutely install a fully functional PHP environment with Homebrew, the [Vagrant](http://www.vagrantup.com) approach is a bit more versatile and I think you should give it a try.

Vagrant allows you to virtualize your development environment, this as several advantages :

* You can have as many different environment you need on your projects.
* You can reuse environments on different projects, and share them with your team members.
* Your local environment can be the same as your production environment.

First you will need to [download VirtualBox](https://www.virtualbox.org/wiki/Downloads).

Then [download Vagrant](http://downloads.vagrantup.com/).

Once the two software are installed, we will try it in a dummy project.

	mkdir dummy && cd dummy
	vagrant box add lucid32 http://files.vagrantup.com/lucid32.box
	vaguant init lucid32
	vagrant up


## Development tools

This is were it starts to be fun. Here are my tools for web development (PHP, Html, JS, CSS, MySQL).
 
* [PHPStorm](http://www.jetbrains.com/phpstorm/) : I've used it a lot last year and it is the most complete editor I've known for web development. It is updated really often. The counterpart is that it can be damn slow on big projects, and can eat all your memory on code introspection (*94€*). 
* [SublimeText 2](http://www.sublimetext.com/2) : I'm forcing myself to use it even for PHP code writing, it's free (*or $59 to get rid of annoying popup while saving*), really light and straight to the point. The only thing I miss is a good PHP autocompletion, although you can have something decent with packages (see bellow) it does not get close to PHPStorm.
* [Coda](http://www.panic.com/coda/) : I'm using it mainly because I already have a license for it, it's useful for a quick edit in a distant server. If you got the money (*$99*).
* [Mou](http://mouapp.com/) : Markdown editor, can be quite useful when writing stuff (like this how to by the way).
* [Sequel Pro](http://www.sequelpro.com/) : nice and free MySQL database management.

### More on Sublime Text 2

If you chose Sublime Text 2 as your main code factory, check out [some packages I use](https://github.com/gabrielpillet/mysetup/tree/master/SublimeText/Packages) :

* Cucumber : syntax highlighting for [Behat](http://behat.com) features.
* DockBlockr : auto expand PHPDoc comment blocks.
* Git : blame, history, state.
* PHP-Twig : twig syntax highlighting.
* SublimeCodeIntel : a little bit of PHP autocompletion.
* SublimeLint : highlight syntax errors.
* ZenCoding : ultimate HTML edition helper, google it to find how awesome it is.



 





