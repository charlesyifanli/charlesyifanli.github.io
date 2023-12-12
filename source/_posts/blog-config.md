---
title: Blog Configuration
date: 2023-12-11 17:01:36
tags:
---

## blog using github and hexo
*The default GitHub-related configurations have been completed.*
```bash
$ npm install -g hexo-cli

$ hexo init blog_name

$ cd blog_name
$ npm install (only download in current dir)

$ hexo g
$ hexo s
```
<br>

modify "_config.yml":

```
......
deploy:
  type: git
  repo: "github url"
  branch: master/main
```

command line

```bash
$ npm install hexo-deployer-git --save

$ hexo clean
$ hexo g / generate
$ hexo d / deploy
```
<br><br>

### note
package:
```
1. node_modules: Dependency packages
2. public: Storage for generated pages
3. scaffolds: Templates for generating articles
4. source: Location for storing your articles
5. themes: Themes
6. _config.yml: Configuration file for the blog
```

tip:
```
Every time 'hexo d' command is executed, it uploads the contents generated locally inside the '.deploy_git' directory. Other files, including those within the 'source' directory, configuration files, and theme files, are not uploaded to GitHub. Without the source files, it's impossible to regenerate the pages.
```
Info: [reference](https://www.jianshu.com/p/358198143668)
