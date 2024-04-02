---
title: LAN Sharing
date: 2023-12-19 19:48:07
tags: 
categories:
- windows config
---

## transfer files within LAN

### PC shared with 

```
1. Select the folder you want to share, right-click and choose Properties, click on Sharing, Advanced Sharing, Share this folder, Permissions, select Full Control. Confirm.
2. Choose Security, Edit, Add, Input Everyone, save and close.
3. Right-click Network, click on Change advanced sharing settings, All networks, turn off password-protected sharing.
```
<br>

### Other PC in LAN

```
In file explorer:
Input: \\ip_address
Input: Everyone
```



## How to use remote desktop

### path

```reStructuredText
Settings => System => About => Advanced system settings => Remote
```

### operation

```reStructuredText
Remote Assistance >> both are right
Remote Desktop >> Only "Allow remote connections to this computer"(No sub item)
```

### set remote desktop user

```reStructuredText
right click win icon >>
computer management => Local Users and Groups => Users
create a new user or use an existed user(recommended: password never expires), double click
Member of => Add => write "remote desktop users" => Check Names =>ok
```

### win+r 

```reStructuredText
mstsc => show options => ip + username (of controllered pc)
```

