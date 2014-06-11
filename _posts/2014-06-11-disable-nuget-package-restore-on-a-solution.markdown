---
layout: post
title:  "Disable NuGet Package Restore on a Solution"
date:   2014-06-11
---

Not too long ago David Ebbo [tweeted](https://twitter.com/davidebbo/status/425493392475168768) the following:

> Every Time someone enables #nuget package restore on a solution, a kitten dies. Learn the new workflow!
    
He then followed up with a blog post titled "[The right way to restore NuGet packages](http://blog.davidebbo.com/2014/01/the-right-way-to-restore-nuget-packages.html)" that, as you can guess, explained the correct way to restore NuGet packages. I suggest you go ahead and read his post as I am not going to cover all of the reasons. OK, now that you've read that, I will explain the problem I ran in to.

## Cleaning your solution

Once you use the "Enable NuGet Package Restore" option in Visual Studio (which the NuGet team now calls the incorrect way), Visual Studio does not give a way to undo that action. This action is not easy to undo, and requires editing the `.sln` file and each `.csproj` file; as well as deleting the `.nuget` directory at the root of your solution. While it is easy to hand edit a single project and solution, removing these items from a solution with a large number of projects is a lot of work. So instead of doing it manually for each solution I work with, I wrote a PowerShell script to do it for me. Here is what I came up with:

<script src="https://gist.github.com/mkchandler/8864804.js"></script>

## Script overview

* Removes the `.nuget` directory and contents from the root of the solution
* Parses the `.sln` file to remove the `.nuget` project section
* Parses each `.csproj` file found within the solution to remove the reference to the `NuGet.targets` file

## Running the script

To run the script on a Visual Studio solution, just pass the `.sln` path to the script as the first argument:

    .\DisableNuGetPackageRestore.ps1 C:\Path\To\Solution.sln

Now you have a clean solution file and can restore packages the proper way. If you are using Visual Studio, it will do it on build. If you are not using Visual Studio, you just need to run the `nuget.exe restore` command. Both of these ways will still use your `packages.config` for each project to restore the needed packages.

## Resources

* The PowerShell script above is provided as a [Gist](https://gist.github.com/mkchandler/8864804)
* [NuGet Docs Restore Command Reference](http://docs.nuget.org/docs/reference/package-restore)
* The NuGet team's guide on [migrating to automatic package restore](http://docs.nuget.org/docs/workflows/migrating-to-automatic-package-restore)
