---
title: Git Configuration
date: 2023-12-07 21:20:32
tags:
---

## first attempt at using Git branching
The main branch is responsible for merging other branches, while other branches are responsible for completing their respective tasks and continuing iterations.

Solution: "A repository corresponds to a sub-branch, create a privileged repository corresponding to all branches, pull all branches in the privileged repository first, then perform a `--no-ff` merge of other branches into the main branch, and push."

Workflow: [reference](https://www.zhihu.com/question/596345017/answer/2997761096)


## command >> git merge --no-ff branch-name
E.g.,<br>
Before merge:
```
  o---o---o---o  master
       \
        o---o    feature
```

Merge with Default (Fast-forward Enabled):
```
  o---o---o---o---o  master (fast-forwarded to feature)
       \
        o---o    feature
```

Merge with --no-ff Flag:
```
  o---o---o---o-------o  master
       \         /
        o---o---o    feature
```

**Note >>**<br>
When merging without the `--no-ff` flag, the `master` branch pointer moves directly to the tip of the `feature` branch. This process doesn't show a distinct merge operation in the commit history.

However, when merging using the `--no-ff` flag, a new merge commit is generated, **preserving the separate histories of both `master` and `feature` branches.**

More info: [reference](https://zhuanlan.zhihu.com/p/452996934)

<br><br>

## ssh: connect to host github.com port 22: Connection timed out

In "~/.ssh/config", 

```
Host github.com
  Hostname ssh.github.com
  Port 443
```

More info: [reference](https://zhuanlan.zhihu.com/p/521340971)

<br>

<br>

## create a new branch based on a specific historical version of the current branch

### Clone the repository locally:

```
git clone <url>
cd your-repository
```

### Create a new branch

```
git checkout -b new-branch-name
```

### Look through the hash value of specific history version

```
git log
```

### Reset the branch

```
git reset --hard commit-hash
```



