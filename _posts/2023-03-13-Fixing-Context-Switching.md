---
layout: post
title: Fixing Context Switching
---

The title of this post may be considered misleading by some.
Let me explain what I mean by telling you about a struggle that I have.
The struggle is that once I learn something well enough for it to be something I
do without thinking, it becomes hard for me to switch and do something else.

The most recent example of this for me was when I started working at Facebook
(now Meta).
When you get hired you get to select your equipment for your laptop and phone.
There was only one choice of laptop for my role: a Macbook Pro.
It was a really nice laptop and lots of people love them.
I don't.
Before all the fans come after me (come at me, bro!) let me explain where the
problem lies:
**completely** and **totally** with me.

I tried for 6 months to convert myself over to the Mac way of doing things.
I tried for 6 months to remember the proper keystroke combinations and shortcuts.
I tried for 6 months to remember that Option is not Alt, Command is not Windows,
Control is in the place of Ctrl but it doesn't do what Ctrl does,
there are no Del, Home, PgUp, PgDn keys (on the laptop),
and there is no escaping that some shortcuts just cannot be done with one hand
or that they are more comfortable if you use two (I'm looking at you, Undo, Cut,
Copy, and Paste!).

You have to understand that I've been using Windows based operating systems since
Windows 3.0 came out.
I even bothered to learn and heavily use the keyboard shortcuts for Windows 3.0
and every OS release since.
That is a lot of finger memory to try to overcome.
I finally gave up and requested a Windows laptop. After it arrived, in less than
10 hours of setup time within one week of regular work, I was back to being fast
and efficient (and less frustrated).

For those of you that started with MacOS, none of this is an issue.
You already have it memorized.
For those that can context switch, you easily use one pattern for Mac and another
for Windows, with an occasional mistake here and there.
I never got to the point where it was an occasional mistake.
It was frustrating.
I don't like being frustrated.
It slows me down, and I'm all about speed.
That is why I use so many aliases when typing at the PowerShell prompt.
I also write Functions for myself based on commands that I tend to use more than
a couple of times, especially if the command is long to type.
Instead of going down a rabbit hole on this topic, just watch for a future blog post.

## Getting back to context switching

One of the things I admire about the developers who worked on Linux and its predecessors
was the brevity and ease of entry for some commands.
My all-time favorite is `ls` for speed and ease.
Right ring finger, left ring finger, Enter.
Boom! Fast!
When I first started with PowerShell, I gravitated to this alias very quickly.
Of course, `dir` still worked and the new `gci` was viable as well, but `ls` is still the fastest.
It has the added bonus of working on the "big 3" operating systems.

Herein lies the problem: in PowerShell, `ls` on Windows is an alias,
whereas `ls` in PowerShell on Linux and MacOS is an application.

Windows `ls` command in PowerShell:
![_config.yml]({{ site.baseurl }}/images/Fixing-Context-Switching-Windows-Ls.png)

Linux `ls` command in bash"
![_config.yml]({{ site.baseurl }}/images/Fixing-Context-Switching-Linux-Bash-Ls.png)

Linux `ls` command in PowerShell"
![_config.yml]({{ site.baseurl }}/images/Fixing-Context-Switching-Linux-Pwsh-Ls.png)

When I'm working in my Windows Terminal I frequently have PowerShell, Linux via
WSL2, and the Azure Cloud Shell open.
![_config.yml]({{ site.baseurl }}/images/Fixing-Context-Switching-Terminal-Tabs.png)

Remember my issue with context switching?
I expect the same results when I'm in PowerShell and running the `ls` command.
Remember that I like to shortcut like mad at the prompt?
Even though `ps` works and returns the processes in Linux and MacOS, it is not
returning a System.Diagnostics.Process object.
Rather, it is running /bin/ps (or, since it is Linux or MacOS, it could be
nearly anywhere) and returning plain text. Yuk!

Of course, I could use the PowerShell-specific alias entries for these commands.
For `ps` the alias `gps` would work fine.
Do you know anyone that uses the `gps` alias?
I've never used it and I've never seen it used either.
In a similar way, the alias `gci` would work fine as a replacement for `ls`.
However, I tend to get burned by running `ps | sort cpu` to find the process
using the most CPU time for two reasons:

1. ps is not ps in pwsh
1. sort is sort, sort of

Yes, I stretched this a bit trying to be funny.
However, the point is there isn't an alias for Sort-Object in Linux or MacOS.
Sort is `/usr/bin/sort`
(again, could be nearly anywhere based on who knows what 'cause Linux/MacOS).

## I am not changing my mind

For the last time, I'm going to remind you that I have an issue with context switching.
I am not going to start using `gci` instead of `ls` to list files,
for `ls` is just too fast.
Plus, when I'm not in PowerShell and I'm in almost any shell,
except for cmd.exe which should not be used anymore (come at me, bro!),
the `ls` command will still work.
In the same way, I'm not switching to `gps` to list the processes.
Not gonna happen.
So what's a PowerSheller to do?
Write some code, of course!

## How I help myself

First, I need to point out that there are times when you will need the functionality
of the built-in commands.
While you could edit your profile and put alias entries in place to overwrite the `ps`
command, you may still need access to this command.
What I've done is taken the commands that I mix up the most and replaced them
with alias entries.
Then, for those commands that are being replaced, I create new alias entries and
add an "l" to them for the original Linux commands.
Of course, I could add the alias entries one after the other,
but where's the fun in that?
Here's my solution that I put in my Linux and MacOS PowerShell profiles:

```powershell
$alias = @{
  'ls' = 'Get-ChildItem'
  'lsl' = '/usr/bin/ls'
  'sort' = 'Sort-Object'
  'sortl' = '/usr/bin/sort'
  'ps' = 'Get-Process'
  'psl' = '/usr/bin/ps'
}

$aliasOutput = foreach ($item in $alias.GetEnumerator()){
  try{
    Get-Alias -Name $item.Name -ErrorAction Stop
  } catch {
    New-Alias -Name $item.Name -Value $item.Value -PassThru
  }
} # end foreach $item in $alias
$aliasOutput | Sort-Object Name
```

The beauty of doing it this way is if an alias already exists this code won't
stomp on it.
It also lists the alias entries.
I did this to remind myself that I set this up.
It is a bit redundant, but it works for me.

Now, with these alias entries in place, I can run ``ps | sort cpu` in any OS and
get consistent results without errors.

> Bonus question for those that are curious: what happens if the output of
`$aliasOutput` is not sorted?

The next shortcut I like to use is the `ll` command in Linux.
Unfortunately, this is not available in PowerShell, nor is it always available
in a Linux distribution.
However, it is in enough of them that it has made its way into my finger memory.
Therefore, I want it available in my PowerShell session.
You might think that the way to solve this is to create an alias for `ll` and
make the command `ls -l` like this:

```powershell
New-Alias -Name 'll' -Value 'ls -l'
```

This will ***not*** work! You will get an error because the Value is neither a
cmdlet nor an application.
In other words, you can't pass parameters in your alias Value.
That's not a problem because we are working with PowerShell.
All we need is a new function:

```powershell
function ll {
  param(
    [parameter()]
    [ValidateScript({
        if (Test-Path $_) {
            $true
        }
        else {
            throw "The path '$_' does not exist."
        }
    })]
    [string]$Path = $PWD
  )

  if($IsLinux -or $IsMacOS){
    /usr/bin/ls -l $Path
  } else {
    Get-ChildItem -Path $Path
  }
}
```

Now, whenever I run `ll` it will return the long list content on a POSIX filesystem
or it will return the standard file and directory contents if run on a Windows based
system.
Unfortunately, this function will do some odd stuff if you try to pass other
parameters to the command.
I could write the code to handle any additional parameters sent to the function,
but I almost always am running the command against the current directory.
Plus, I still have `lsl` available to pass any parameters as I need.

## Conclusion

Now, when I'm entering commands at the PowerShell prompt in Windows, Linux, and
MacOS, I'm getting consistent results while still having the standard commands
available just by adding the "l" character.
This change does have the possibility of messing up some scripts that rely on the
standard commands so please be aware of this potential issue.
However, I have not run into this issue since I'm running PowerShell commands
in my PowerShell scripts and I can always be explicit for the command paths.
I hope you got some use out of these tips for entering commands at the console
and getting consistent results quickly and efficiently.

## Shortcut your life

![_config.yml]({{ site.baseurl }}/images/ShortcutYourLifeBlogSized.png)
