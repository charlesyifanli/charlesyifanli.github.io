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