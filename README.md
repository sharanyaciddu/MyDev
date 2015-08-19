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

### Install Basic packages


The following packages are super useful:
```
brew install wget
brew install git
brew install jenkins
```

