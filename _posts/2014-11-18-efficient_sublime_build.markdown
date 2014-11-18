---
layout: post
title:  "Efficient use of Sublime Text build systems"
date:   2014-11-18 14:01:39
categories: code sublime
---

As you may know you can define custom build systems in Sublime Text.
It is very useful and should look like this :

    {
        "cmd": ["make", "-j8", "config=debug64"],
        "working_dir": "/home/gogoprog/code/myproject/build/",
        "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$"
    }

The problem is that they are project-specific when written like this so I had plenty of these files on my system...

My projects have most of the time the same structure : the Makefile in xxx/build. So something must be done!

And there is a simple solution for that : the use of variables!

[Build systems reference]

You could use ${project_path} but it didn't fit my case so I used ${project_base_name}.

Now I have 2 main sublime text build systems :

debug32:

    {
        "cmd": ["make", "-j8", "config=debug32"],
        "working_dir": "/home/gogoprog/code/${project_base_name}/build",
        "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$"
    }

debug64:

    {
        "cmd": ["make", "-j8", "config=debug64"],
        "working_dir": "/home/gogoprog/code/${project_base_name}/build",
        "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$"
    }

Now it is way easier to use!

[Build systems reference]: http://sublimetext.info/docs/en/reference/build_systems.html

