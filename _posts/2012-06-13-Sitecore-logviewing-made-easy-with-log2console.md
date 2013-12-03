---
layout: post
title:  "Sitecore logviewing made easy with log2console"
date:   2012-06-13 10:10:00
categories: deploy CI
---

Today i saw this tweet from [@kiranpatils](http://twitter.com/#!/kiranpatils)
>My new #Sitecore shared source module -- SCLogExplorer -- easier and faster way to analyze #sitecore log files --http://trac.sitecore.net/SCLogExplorer

 And that make me think I should share the tool I am using, when I am developing.
Log2Console
--

[Log2Console](http://log2console.codeplex.com/) is using the different logging library's ability to log over TCP or UDP.

Sitecore is using log4net as logging engine, where there are implemented [UDP and TCP appenders](http://logging.apache.org/log4net/release/config-examples.html).
![Create adapter](/assets/2012-06-13-Sitecore-logviewing-made-easy-with-log2console/1.png)

It can filter on different loggers, so you can filter out any loggers you don't want, eg. Sitecore Diagnostics, analytics and more.

![Filter](/assets/2012-06-13-Sitecore-logviewing-made-easy-with-log2console/2.png)

Log2Console can also search in the log, and filter on what level off logging you want to see

![Filter](/assets/2012-06-13-Sitecore-logviewing-made-easy-with-log2console/3.png)

How to setup a UDP receiver 
---

In log2console, there is a button on the top, named receivers.
In that window, press add, and pick UUDP (IP v4 and v6)

Now you have added a receiver, and can configure that receiver.
Just leave it as default, and pick up the configuration from the sample configuration.

How to configure Sitecore
---

Open up the web.config from the Sitecore solution you want to receive logs from.

Find the log4net section.
And insert the sample configuration, like i have done in the code below, between the log2console comments
One thing you need to modify, is the remote address it sends log messages to. 
Change it to 127.0.0.1, because at some reason localhost ain't working.
You also need to setup a logger to use the appender you just inserted.
I'm using root, so I will receive everything.
Now launch the browser, and start up the website, and see log messages 

{% gist 2919560 web.config.Sitecore %}

One more thing
---

You don't want this to be in production. 
If you like me, using config transform from msbuild package pipeline, you can insert this code snippet in your web.config transform file.

{% gist 2919560 web.transform.config %}

I hope you like this little tutorial on how to use log2console, it has a lot more features that i haven't used, so if you find somthing good, let the community know about it.

Oh and one thing i hate with the original Log2Console, is using windows 7's way to show progress state, to show that there is log messages coming in - So i made a fork making that an option. 