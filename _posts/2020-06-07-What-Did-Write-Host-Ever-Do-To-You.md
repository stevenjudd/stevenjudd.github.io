---
layout: post
title: What Did Write-Host Ever Do To You?
---

You may have heard it said that using Write-Host kills puppies.
You may have even had that type of hysterical hyperbole transmitted to you during one of my PowerShell classes or by one of the PowerShell aficionados in the community.
Then, some of you may have been brazen enough to look at some of my scripts and then pointed fingers at the author (me) and said, "Ha! You don't even follow your own guidance!"
(See how smart I make you sound even while you are trying to cast aspersions.) 😉

However, there are reasons to use Write-Host, and if you have taken one of my classes or gotten advice from me directly then you will already know that it, along with Write-Information, are good tools to return feedback to the user of a script or function without polluting the Output stream.

I assume we are all on a journey to learn more and improve our skills.
Therefore, I present to you the following bold proclamation:

- Write-Output is more evil than you ever imagined Write-Host to be and should ***NEVER*** be used henceforth.

For those of you that may have fainted at the very thought of what I just proposed, I hope you are feeling better now.
To support this bold proclamation I present to you the following article by Mark Kraus that lays out why you should avoid the use of Write-Output:

<https://get-powershellblog.blogspot.com/2017/06/lets-kill-write-output.html?m=1>

The TL,DR:
Write-Output is essentially a wrapper for the Cmdlet.WriteObject() method, thus each invocation has a cost to performance.
It is better to put your objects directly on the output stream.

Please let me know your thoughts and questions.
I hope this information is valuable and will help us all be better script writers.
