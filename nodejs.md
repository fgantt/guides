OS X Install
=======================
* To uninstall an existing node.js install:

 https://gist.github.com/nicerobot/2697848

* Install new node.js from PKG distribution:

 https://nodejs.org/download/
 
* Confirm node and npm installation
```bash
 node --version && npm --version
``` 
* Setup npm to install global packages in home folder:

 https://github.com/sindresorhus/guides/blob/master/npm-global-without-sudo.md

Create directory:
```bash
 mkdir ${HOME}/.npm-packages
```

In ~/.bash_profile add:
```bash
 ## Node
 export NPM_PACKAGES=${HOME}/.npm-packages
 NODE_PATH="$NPM_PACKAGES/lib/node_modules:$NODE_PATH"
 PATH="$NPM_PACKAGES/bin:$PATH"
 # Unset manpath so we can inherit from /etc/manpath via the `manpath`
 # command
 unset MANPATH # delete if you already modified MANPATH elsewhere in your config
 MANPATH="$NPM_PACKAGES/share/man:$(manpath)"
```

Create or add to $HOME/.npmrc
```
 prefix=${HOME}/.npm-packages
```
 
* Reload bash profile 
```bash
source ~/.bash_profile
```

* Try it:
```bash
 npm install -g npm@latest

 npm install -g jshint
```

* If you start getting EACCES or other permissions errors from npm, check the owner of ~/.npm. To reclaim (ref - http://stackoverflow.com/questions/16151018/npm-throws-error-without-sudo):
```bash
 sudo chown -R $(whoami) ~/.npm
``` 

  
