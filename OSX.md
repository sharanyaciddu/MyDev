# Mac OS X
Custom recipe to get OS X running from scratch, setup applications and my developer environment. 
I use this to keep track of the important software and steps required to have a functioning system after a fresh install.

## Homebrew

You are going through some source code and found the link to a resource on the web. You wanted to download and inspect it. Immediately you dab in the following into your OSX terminal:
```
wget http://foobar/foobar.txt
```
You expect the file to be downloaded onto your disk. No it doesn't. You see the following error message:
```
-bash: wget: command not found
```
What!! Doesn't OSX have everything that that is available in Linux?

No. It doesn't. `wget` is a [GNU](https://www.gnu.org/home.en.html) package and there are so many basic packages in Linux missing from OSX. Installing each of these individual packages is not trivial either. Here comes the savior.

[Homebrew](http://brew.sh/) - The missing package manager for OSX.

### Install Homebrew

Paste the following into your OSX Terminal:
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Install packages

```
brew install wget
brew install curl
brew install git
brew install jenkins
brew install maven
brew install ant

```

## Homebrew Cask
[Cask](http://caskroom.io) is the missing Mac apps manager for OS X. Don't waste time anymore with dragging'n dropping. Use the power, the speed and the simplicity of Homebrew to manage your Mac applications. Friendly.

### Install Cask
```
brew install caskroom/cask/brew-cask
```

## Install apps
```
brew cask install caffeine
brew cask install google-chrome
brew cask install google-drive
brew cask install google-hangouts
brew cask install iterm2
brew cask install sublime-text

```


