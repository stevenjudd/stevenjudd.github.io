---
layout: post
title: My PowerShell Journey
---

In this post I am going to give some details around my introduction to PowerShell and what learning PowerShell and my involvement with the PowerShell community has done for me.

## The backstory

The first version of Windows I ever used was Windows 2.1 in 1990. The first PC I bought, an IBM PS/2 386SX16, came with Windows 3.0. After graduating in 1992, my first computer job came in 1993 where I worked on a help desk doing phone support, mostly thanks to learning Word and Excel on my (now) Windows 3.1 PS/2 computer. I became a Windows Administrator in 1994, managing System Management Server 1.0 running on Windows NT Server 3.5. I received my MCSE on Windows 3.51 in 1997. To this point in my career I had taken exactly one computer class: Introduction to Computers in Business. In this class I learned the basics of DOS, Lotus123, and dBASE. The reason I mention the above history is it shows that I did not have any formal development or Computer Science background.

## First look at PowerShell

I started looking at Monad around Beta 2 and subsequent pre-release versions including the official release. Frankly, I didn't understand it. I was an administrator not a developer and the concepts of objects and APIs did not resonate with me. In 2008 I took a PowerShell class taught by a Microsoft employee and thought it was OK, but wasn't sure it was going to replace my entrenched knowledge and library of VBScript based scripts.

## Looking at the future

At that time, I was the lead SharePoint administrator, among other duties. When SharePoint 2010 was about to be released I noticed that many advanced administrator functions were only available via PowerShell. This was also true for Exchange Administration. I felt like this was the direction Active Directory, as well as some other products, were heading. It was becoming clear to me that PowerShell was the direction advanced administration was headed. I was at a junction in my administration career.

## The path I took was a shortcut

I had been using a keyboard shortcut that opened a command window for at least 8 years. So I made a decision and switched my keyboard shortcut from opening CMD.EXE to PowerShell.exe, a shortcut I'm still using today. It wasn't all smooth sailing. At first, the transition from %username% to $env:username and %computername% to $env:computername were hard. Plus, I had all this VBScript knowledge and example scripts to draw on. But I knew that I had to get past the learning curve and the only way to do that was to work exclusively in PowerShell.

## Not all shortcuts are easy

It was still a struggle because I didn't know about objects and why they mattered. PowerShell was simply a replacement for a console window. New commands, same basic results. Also, since it was PowerShell 2, the ISE was not very good. In fact, the three pane application was downright confusing. If you never experienced the ISE for version 2, consider yourself lucky. It was around this time I found the PowerGUI tool. This allowed for much faster script writing, and because it was free I didn't have to justify an expense to purchase a PowerShell editor.

## My first "ah ha!" moment

Since I had been using VBScript and batch files for quite a while, I was still trying to get used to working in PowerShell. I had VBScript examples for handling repetitive actions. One of these actions was sending an email from a script. Since I was converting my work to PowerShell, I needed a way to send email from PowerShell. That's when I found the Send-MailMessage cmdlet. "You mean I only need one command to send email? I don't need multiple lines of code like VBScript?" That alone convinced me that PowerShell was a game changer for how I will get work done going forward.

## Gaining momentum

In 2012, a couple of coworkers had been working to develop a one day training class to introduce people to PowerShell. I got involved with them and began working to improve the Intro to PowerShell class and materials. They asked me if I would want to help them develop the next class, a PowerShell 201 class, to help take our organization's PowerShell training to more advanced topics. We worked together to decide on the outline of topics to cover and we chose the sections we were going to write. Then we reviewed each others' sections and printed the manuals. We all helped teach the first two-day class in December, 2013. We have since added more material, expanded to a three-day class, and I have been teaching this class about once or twice a year. It is amazing how much you learn when you are teaching.

## Expanding my world

In 2019 I attended the PowerShell + DevOps Global Summit. It was a great experience to meet with and learn from people that are just as passionate about PowerShell as I am. Not only were they passionate, they were highly skilled and very knowledgeable. Plus, they were friendly and willing to share. The experience inspired me to continue to deepen my knowledge and to get involved with the broader community. I am still ramping up my community involvement. One way that I do this is to regularly participate in the PowerShell bridge community on Discord, IRC, and Slack.

## What did learning PowerShell do for me?

First of all, let me make it clear that PowerShell is a tool. A powerful, flexible tool, but a tool nonetheless. It will help you get something accomplished. What it helped me do is get more done with less time and effort, as well as greater accuracy. Answering hard questions quickly makes you seem like a genius, or at least might impress a coworker or leader. Being able to demonstrate and quantify improvements to the business will engender you to management. Sharing your knowledge and trying to bring others up along with you will make you a team player.

Let me explain how this played out for me personally. I work in the energy sector. Times were great when prices were high, up until 2015. Then when prices came crashing down, times were not great. We have had layoffs at our company every year starting in 2015 through 2019, excepting 2017. Not minor cuts either. The smallest cut was 2019 at 10%. The largest was 33%. That is a lot of people exiting the organization in a short amount of time.

It is my belief that my willingness to learn, share, and automate that has kept me from being laid off. There always are other factors in play, but I think being able to demonstrate a tangible return, as well as lifting others up was the difference maker. All of us that are involved in automation are able to "do more with less," a common phrase uttered by business people everywhere. My coworkers that developed the training material with me are still employed as well. They are good at their jobs (really good, in my opinion), but I think the automation skills make the difference when the management team was having to make the hard decisions about who to keep.

On a more positive note, the time I have spent with the PowerShell community has not just given me more knowledge and skills. It has allowed me to develop new friendships and contacts in other industries, states, and countries. I have been able to meet and have conversations with some of the most influential people involved with PowerShell, including the inventor of PowerShell, Jeffery Snover. I have met and hung out with the team that is continuing to develop PowerShell, and they are really great people. That has been the true blessing of the past few years. 

---

## Summary

No matter where you are starting from you can learn how to use PowerShell. Hopefully, you will quickly see the value of expanding your understanding of how to effectively use PowerShell to accomplish your work and become a more capable and more valuable professional. I am continuing to learn more about PowerShell via other PowerShell enthusiasts, powershell.org, PluralSight, Twitter, Channel9, PowerShell.com, books, conferences, and more (because there are always more ways to learn). I enjoy sharing my experience with others that want to learn as well. I hope this inspires you to either start or continue your journey and get the most out of your knowledge and skills.