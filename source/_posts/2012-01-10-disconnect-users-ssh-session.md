---
layout: post
title:  "Disconnect user's SSH session"
date:   2012-01-10 12:01:01
comments: true
categories: discoveries
tags: linux ssh
---


With my VPS I sometimes encounter a situation when I try to open a file with Vim, but it tells me the file has already been opened by someone else. This “someone else” is another myself, logged in via SSH from my laptop, which has been suspended (SSH sessions are not being disconnected when you suspend). An easy way to disconnect myself, logged in from the laptop, is using pkill.

```
$ pkill -KILL -u <username>
```

That’s it. SSH session has been disconnected and I can now open the desired file.