---
layout: post
title:  "Fixing the 'MOZILLA_FIVE_HOME not set' in Ubuntu"
date:   2011-12-25 12:01:01
comments: true
categories: discoveries
tags: aptana eclipse ubuntu xulrunner
---


There is quite a lot of noise regarding this error in the Internet. It is being triggered by Eclipse's (and Eclipse-based products') SWT, whenever it tries to generate a 'browser' window (like the one used when you do git commit in Aptana).

The root cause of this error is that Eclipse's SWT cannot find Mozilla's Xulrunner, which it uses to draw 'browser' windows. It seems that the problem appeared with Firefox 3.0 (at least I've found a post of a guy who wrote he started to see this after his Firefox upgraded from 2.x to 3.0). For some reason SWT does not support Xulrunner of versions greater than 1.9.2.

Well, all the solutions found on StackOverflow, forums, bug trackers seem invalid. They all suggest to define the `MOZILLA_FIVE_HOME` environment variable and point it to the Xulrunner installation (wherever it's installed, with the requirement that the directory should contain libxpcom.so). In my case the result was that even the downloaded and extracted old Xulrunner 1.9.2 refused to work.

Then, on the Eclipse SWT FAQ page I found out that you can define custom path to Xulrunner Eclipse should be using. This is done with org.eclipse.swt.browser.XULRunnerPath option. But my downloaded and extracted Xulrunner distribution refused to work this way.

Then I started searching for an Ubuntu package of that old Xulrunner 1.9.2 (thought it could be that the lib should actually reside in the lib path). Since Xulrunner seems no longer being distributed apart from Firefox (at least in Ubuntu), there is not separate Xulrunner package for Ubuntu in the repositories. But I was lucky to find one for Oneiric on Launchpad here

So, basically, the steps to fix the error are the following:

- Download and install Xulrunner deb package from the Launchpad page above
- Add `-Dorg.eclipse.swt.browser.XULRunnerPath=/usr/lib/xulrunner-1.9.2.17` option to your `eclipse.ini` (`AptanaStudio3.ini`)

That should fix the problem.

Thanks to Bruno Carlin for the [insight](http://aerdhyl.eu/blog/2011/12/Aptana-eclipse-and-xulrunner.html)
