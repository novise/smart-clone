# Git clone manager for multiple accounts

## Prerequisites

At the moment this is only built to handle [Github](github.com) and [Bitbucket](bitbucket.com)

For a given profile you can configure both a github and bitbucket account, the appropriate one will be used when cloning.

There is a fair bit of set up needed to get this to work. An install script is in the works but might take some time. If you want to contribute one feel free to do so.

Here are the steps reqired to get this to work.


## Installation
The clone script needs to be put in an appropriate folder that is on the $PATH and set as executable
### SSH config
 Add ssh configs for all the accounts you wish to use. Adding a postfix after the Host in the following manner. 
```
Host gitbub.com[POSTFIX]
    HostName github.com
    User [USERNAME]
    IdentityFile ~/.ssh/[Key name]
``` 
### git-clone config
 Create the configuration for the git-clone script, it is expected to be called ```cloneConf``` and is expected to be found in the directory ```$HOME/.config/``` and is expected to follow the below structure. One configuration can contain a setup for both github and bitbucket or olny one of them.

 ```
 User [Name]
		Name “Your Name” 
		Email “Your Email”
		Bitbucket “[POSTFIX]”
		GitHub ”[POSTFIX]”
```

You can now use the script as '```git-clone [GIT SSH URL]```'

### Optional
To enable more consisten use of ```git-clone``` in a similar manner as the regular '```git clone ...```' add the following to your bash config file. This will hijack the regular git commands and override it if it is the clone command, to use the git-clone script.

``` 
alias git=betterclone

betterclone () {
	if [ “$1” = “clone” ]; then
  		git-clone “$@”
	else
  		/usr/bin/env git “$@”
	fi
}
```