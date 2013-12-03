---
layout: post
title:  "Adding extra files to a deployment package in Visual Studio 2012"
date:   2012-10-01 20:58:00
categories: 
---
Today i ran into that problem again.
In vs2010 the property "CopyAllFilesToSingleFolderForPackageDependsOn" contains targets, to add files that would go into a publishing package.

In Visual Studio 2012 it is renamed to "CopyAllFilesToSingleFolderForMsdeployDependsOn", it took some time to find the solution, so now i hope to help everyone that got the same problem.
Working Sample
This sample includes all the files from "$(SolutionDir)\files" into the package that can be deployed.

{% gist 3811185 %}