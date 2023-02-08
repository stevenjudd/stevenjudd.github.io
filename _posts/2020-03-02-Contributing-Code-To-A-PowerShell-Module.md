---
layout: post
title: Contributing Code To A PowerShell Module
---

If you find a PowerShell Gallery project has *almost* everything you need except
for one little feature, you can (hopefully) modify the code on your own machine
and then use it for yourself.
However, that does not do much for the community of users that may also want to
use your enhancement.
Here is an example of how to add to a project that is already on PowerShell
Gallery.

First, you need to find the module code.
Hopefully, the code is in a public repo, like GitHub.
The way I found the code for my example was to take the author name from the
PowerShell Gallery and search GitHub for the same author.
I was able to find a user on GitHub with the same name, so I went to their
GitHub page and looked at their projects.
There, I found a project with the same name as the Module on the Gallery.
I checked the code for a couple of the functions and it was the same code as
the downloaded module.

The good news is that since it is in GitHub and I have a GitHub account, there
is a means for me to work with the code.
However, even though I have found the source code, I do not have rights to 
modify the repo of someone that I don't know (surprise).
I would have to be given permissions to be able to modify the repo by someone
that owns the repo.
There is a way to work with the code without being granted permissions.
This is where you "Fork" the repo.
This will create a copy of the project in your GitHub profile.
All of the desired changes will be made to the forked repo.

Once I have the code in a local git repo, the first step is to create a branch
to work from.
This should always be your first step: create a branch to work from.
Any decent remote git repo will have branch policies in place and will not
allow you to push directly into the master branch.

Make the changes you intend to make into the newly created branch.
Be sure and keep your changes focused and create more branches if necessary.
Comment your changes and pushes so the original author will be clear about the
changes you have made and are asking to be merged into their project.

Once you are satisfied with your changes it is time to make a pull request to
the original project.
First, push your branch to your forked repo.
I did this at the command line using the following git command:

```git push --set-upstream origin <name of branch>```

If you are using an IDE/ISE that is git aware, like VSCode, you can use the
tool to push your branch to your remote GitHub repo.

Next, go to your GitHub project, and open a pull request to the original
project.
Make sure that you provide the reason and the major details for the changes to
the original project in the comments for the pull request.
In other words, make it easy for the owner of the original project to know why
you are requesting the delivered changes to their project.
Once you are satisfied with the message, create the pull request.

It is now up to the original project creator to accept your pull request.
Only those with write access to the original repo can merge pull requests.
If it is a project that you are working on with a team of other people you may
have granted more people access to write to the project.
However, for most cases on GitHub, you will not have write access.
Also, many projects, like docs.microsoft.com, have reviewers and workflows and
approvals and tests and more that have to be addressed before your pull request
will be approved.
So keep an eye on your email for the notification that your pull request has
been approved.

Congratulations! You have not only just made your life better, but you have made
life better for everyone that comes along after you. Plus, you helped the
original developer improve their product, for which I'm sure they are thankful.