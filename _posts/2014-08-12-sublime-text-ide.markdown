---
layout: post
title:  "Sublime Text as a C/C++ IDE"
date:   2014-08-12 14:00:39
categories: cpp code ide
---

How to use Sublime Text 2 as a full C/C++ IDE?

For that I needed at least 2 things :

Ability to double-click on gcc results to get at the right position in the file.
Debugging with breakpoints, callstack, threads, etc…
For the first one it was easy as it is already included in the default ‘make’ build system. So I just needed to write a custom build system:

{% highlight json %}
{
    "cmd": ["make", "-j4"],
    "working_dir": "/home/gogoprog/code/myproject",
    "file_regex": "^(..[^:]*):([0-9]+):?([0-9]+)?:? (.*)$"
}
{% endhighlight %}

working_dir points to where your Makefile is
file_regex is important to parse gcc output and be able to go to errors
For the second point simply install the SublimeGDB package then go to “Project” -> “Edit Project” and fill your project settings :


{% highlight json %}
{
    "folders":
    [
        {
            "path": "/home/gogoprog/code/myproject"
        }
    ],
    "settings":
    {
        "sublimegdb_workingdir": "/home/gogoprog/code/myproject",
        "sublimegdb_commandline": "gdb --interpreter=mi /home/gogoprog/code/myproject/mybinary"
    }
}
{% endhighlight %}

And that’s all! The default keys for SublimeGDB are the same as in Visual Studio (F5:debug, F9:place-breakpoint, F10:step-over, …)