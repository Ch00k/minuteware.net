---
layout: post
title:  "VMware Player and VMware VIX. The specified version was not found"
date:   2012-03-09 12:01:01
comments: true
categories: discoveries
tags: linux player vix vmware
---

Having VMware Player 4.0.2 and VIX 1.11 (the latest to the time of writing this) installed, it appeared that they don’t play well together. Trying to run my VM I was getting The specified version was not found error.

```	
$ vmrun -T player start ~/vmware/gentoo/gentoo_x86.vmx nogui
Unable to connect to host.
Error: The specified version was not found
```

A solution to this problem is quite simple. Actually, as far as I can tell, this is a bug. There is a file `/usr/lib/vmware/vixwrapper-product-config.txt`, which is installed along with VMware Player, and maps VMware Player/Workstation versions to their corresponding VIX API versions. The problem is that the version of VMware Player in this file is 4.0.0, whereas I installed 4.0.2.

```
player 14 vmdb 4.0.0 Workstation-8.0.0-and-vSphere-5.0.0
```

I suspect VMware guys just forgot (and are sometimes forgetting, as this problem has been seen before) to update this file when releasing new version. So what you’ve got to do is to substitute 4.0.0 with the verion of Player you have installed.