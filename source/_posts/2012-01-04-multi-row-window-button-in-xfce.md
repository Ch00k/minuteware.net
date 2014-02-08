---
layout: post
title:  "Multi-row window buttons in Xfce"
date:   2012-01-04 12:01:01
comments: true
categories: discoveries
tags: linux xfce
---


To make the Xfce Window Buttons applet (or simply the Taskbar, as all of us are used to call it) multi-row, add the following to `~/.config/xfce4/gtkrc` (create the file if it doesn’t exist):

```
include "/usr/share/themes/greybird/gtk-2.0/gtkrc" # Change 'greybird' to whatever Xfce theme you're using
 
style "xfce-tasklist-style"
{
    XfceTasklist::max-button-length = 192
    XfceTasklist::max-button-size = 16 # Make sure that this value is at least two times less than the panel size
    XfceTasklist::ellipsize-mode = PANGO_ELLIPSIZE_END
    XfceTasklist::minimized-icon-lucency = 50
    XfceTasklist::menu-max-width-chars = 24
}
class "XfceTasklist" style "xfce-tasklist-style"
```

After you relogin, your panel should look like this:

![multi-row](/assets/window_buttons.png)