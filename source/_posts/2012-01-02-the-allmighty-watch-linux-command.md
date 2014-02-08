---
layout: post
title:  "The allmighty `watch` Linux command"
date:   2012-01-02 12:01:01
comments: true
categories: discoveries
tags: linux monitoring
---


I was searching for a way to make some kind of a live memory usage monitoring in Linux when I found watch. I wonder why didn’t I ever knew about it! It’s damn useful! You can monitor literally everything with watch.

Here are some scenarios you may use if for:

Watch for changes in a directory:
	
`$ watch ls -la`

Watch for any Java program being started/stopped:
	
`$ watch -n 1 "ps ax | grep java"`

I used watch for memory usage monitoring:

`$ watch -n 1 free -m`

`$ watch -n 1 cat /proc/meminfo`