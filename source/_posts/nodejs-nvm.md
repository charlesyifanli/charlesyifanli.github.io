---
title: Nodejs
date: 2023-12-10 18:41:42
tags:
---

## change npm registry

### common command

``` bash
npm config get registry

npm config set registry https://registry.npmmirror.com/(taobo)

npm config set registry https://registry.npmjs.org/
```


## nvm

### what is "nvm"

NVM (Node Version Manager) is a tool that manages multiple Node.js versions.

### common command

``` bash
nvm ls - View currently installed versions

nvm install <version> 

nvm use <version>

nvm list available - Display a partial list of available versions for download

nvm uninstall <version> 

nvm alias - Add aliases to different version numbers

nvm unalias - Remove defined aliases

nvm reinstall-packages <version> - Reinstall globally installed npm packages for a specified version in the current Node environment
```

More info: [reference](https://zhuanlan.zhihu.com/p/549256854)
