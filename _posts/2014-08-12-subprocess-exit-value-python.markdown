---
layout: post
title:  "Exit value of a subprocess in Python"
date:   2014-08-12 14:23:39
categories: code python
---

os.system doesn’t return the exit code directly but a tuple containing its pid and exit status indication: a 16-bit number, whose low byte is the signal number that killed the process, and whose high byte is the exit status (if the signal number is zero); the high bit of the low byte is set if a core file was produced.

So that means you have to do the following:

{% highlight python %}
tuple = os.system("your_command");
exit_code = tuple >> 8
{% endhighlight %}

[Ref python](http://docs.python.org/3/library/os.html#os.wait)