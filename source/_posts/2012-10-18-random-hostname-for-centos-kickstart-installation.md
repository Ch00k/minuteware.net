---
layout: post
title:  "Random hostname for CentOS Kickstart installation"
date:   2012-10-18 12:01:01
comments: true
categories: discoveries
tags: linux xfce xubuntu
---

A cool option to install CentOS (and some other distros) is to use [Kickstart](http://fedoraproject.org/wiki/Anaconda/Kickstart). One thing I found missing in Kickstart is a possibility of adding some randomness to my installation out of the box. For example if deploying many CentOS virtual machines from one kiskstart file I wanted each of them to have a unique hostname. This is not possible to do with kickstart’s network `--hostname=<my-hostname>` option because it does not accept any code snippets. Instead this can be done with Kickstart’s `%pre` script.

Create a `%pre` section like so:

```
%pre
echo "network --hostname=`echo centos-$RANDOM$RANDOM`" > /tmp/pre-hostname
%end
```

Then somewhere in the main Kickstart section place this:

```
%include /tmp/pre-hostname
```

This command will include the `network --hostname` option into your main Kickstart section and you will end up with a hostname like `centos-2656530171`