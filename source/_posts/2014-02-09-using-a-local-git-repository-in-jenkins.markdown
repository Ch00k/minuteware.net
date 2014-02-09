---
layout: post
title: "Using a local Git repository in Jenkins"
date: 2014-02-09 08:05:33 +0200
comments: true
categories: discoveries
tags: git jenkins
---

Even if you want to run a Jenkins server locally for testing purposes to correctly configure a job Jenkins still needs to fetch the source from a repository. With Git this can be easily done without configuring a Git server. Just specify the path to a local Git repo with `file://` protocol like this:

```
file:///home/ay/dev/projects/my_new_project
```

Then input this path as repository URL in Jenkins.