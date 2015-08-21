<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  
- [Setup Jenkins on OSX using Homebrew](#setup-jenkins-on-osx-using-homebrew)
  - [Installation](#installation)
  - [Creating a jenkins user](#creating-a-jenkins-user)
    - [Create a new hidden user named *jenkins* in OSX](#create-a-new-hidden-user-named-jenkins-in-osx)
    - [Set the home directory of the user](#set-the-home-directory-of-the-user)
  - [Create the daemon](#create-the-daemon)
    - [Create the plist file](#create-the-plist-file)
    - [Load the daemon](#load-the-daemon)
  - [Create an ssh key](#create-an-ssh-key)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Setup Jenkins on OSX using Homebrew

## Installation
* Make sure you have [Homebrew](http://brew.sh/) installed. 
* Install jenkins using brew
```
brew install jenkins
```
* Jenkins runs as a standalone.
* You can start jenkins using the command ```jenkins```.
* Check if you are able to access Jenkins using [http://localhost:8080/](http://localhost:8080/).

## Creating a jenkins user
### Create a new hidden user named *jenkins* in OSX
```
sudo dscl . create /Users/jenkins
sudo dscl . create /Users/jenkins PrimaryGroupID 1
sudo dscl . create /Users/jenkins UniqueID 300
sudo dscl . create /Users/jenkins UserShell /bin/bash
sudo dscl . passwd /Users/jenkins $PASSWORD
```

### Set the home directory of the user
```
sudo mkdir /var/jenkins
sudo dscl . -append /Users/jenkins home /var/jenkins
sudo dscl . create /Users/jenkins NFSHomeDirectory /var/jenkins
sudo chown -R jenkins /var/jenkins
```

## Create the daemon 
Mac OS uses launchd to control daemons and agents. It’s pretty easy to create a launch daemon.

### Create the plist file
Create the file ```/Library/LaunchDaemons/org.jenkins-ci.plist``` with the following content,
based on the plist from the [homebrew jenkins formula](https://github.com/Homebrew/homebrew/blob/master/Library/Formula/jenkins.rb). 
You may need to update the version number in the ProgramArguments.

```
sudo vim /Library/LaunchDaemons/org.jenkins-ci.plist
```

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>Jenkins</string>
    <key>ProgramArguments</key>
    <array>
      <string>/usr/bin/java</string>
      <string>-Dmail.smtp.starttls.enable=true</string>
      <string>-jar</string>
      <string>/usr/local/Cellar/jenkins/1.624/libexec/jenkins.war</string>
      <string>--httpListenAddress=127.0.0.1</string>
      <string>--httpPort=8080</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>UserName</key>
    <string>jenkins</string>
  </dict>
</plist>
```
### Load the daemon
```
sudo launchctl load /Library/LaunchDaemons/org.jenkins-ci.plist
```

## Create an ssh key
```
sudo -u jenkins ssh-keygen
```
