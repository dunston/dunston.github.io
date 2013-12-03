---
layout: post
title:  "Friendly message to the visitor when deploying"
date:   2012-05-29 20:58:00
categories: deploy CI
---

When using CI(continuous integration) you can end up with a site showing "503 Service Unavailable", if you, like me are shutting down the application pool, to clean up temp files and unused files.

To make a more informative and user friendly message - when the application pool is down, a app_offline.htm file is required.
When this file is in the web root, IIS will automatically shut down the application pool, and release all file dependencies.

So first make app_offline.htm, and place it somewhere (I got it under my solution directory, in a folder called Build)

Now it just need to be deployed instead of the step where the application pool is being stopped.

I'm using teamcity to perform our CI, and got a step that stops the application pool.
So I'm replacing that step with a msdeploy step that only deployes app_offline.htm


and when the deployment is done, I got a step that removes the app_offline.htm file.


Now there is a friendly message telling the visitor its down for maintenance, and will be back soon, and refresh the page for the visitor.