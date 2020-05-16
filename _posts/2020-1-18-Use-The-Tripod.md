---
layout: post
title: Use the Tripod For PowerShell Stability
---

If you are wanting to learn how to use PowerShell then you better know about "The Tripod." This is what I call the three cmdlets that you will most likely use more than any other cmdlets. They are:

* Get-Command
* Get-Help
* Get-Member

Let's take a quick look at these three cmdlets and explain why they are used so frequently.

## Get-Command

Get-Command will list the commands that you have loaded in your PowerShell session. If the command you are wanting to run is not listed, then you will need to make sure it is loaded or available before you can use it. (Thank you Captain Obvious.) I am not going to go over how to get commands installed in this post. If you want to know more, look at the **Find-Module**, **Install-Module**, and **Get-Module** cmdlets.

You can search for part of the command that you are looking for. This is helpful if you don't know what command you need. For example, if you want to know if a file exists you might try to run **Check-File**, but that won't (shouldn't) work because Check is not a valid PowerShell verb. So, you guess again: **Test-File**. This won't (shouldn't) work either, but at least it is a valid verb. So, you use Get-Command:

```powershell
Get-Command test-*
```

This returns a list of commands that start with the "Test" verb, including one that might work for checking if a file (item) exists: **Test-Path**. You also see **Test-Connection** and most likely more commands. But how do you know if Test-Path is the correct command? The next leg of the tripod:

## Get-Help

Once you know what commands you have available to you via Get-Command, you will need to know how to use the command. Get-Help will explain the purpose of the command, what parameters are avaiable, what parameters are required or optional, the syntax options for the command, some examples on how to use the command (hopefully there are good examples, which I have not always found to be the case), and usually you will get the Inputs and Outputs for the command.

If you run Get-Help against Test-Path, you will get the basic information for the cmdlet:

```powershell
Get-Help Test-Path
```

 The Synopsis tells you that Test-Path "Determines whether all elements of a file or directory path exist." Bingo! That is exactly what you were looking for. The Syntax section tells you more about how to execute the cmdlet. We will not go into explaining the Syntax, just know that this is valuable information and you should spend time learning how to read it.

>**Pro Tip**: running Get-Help does not give you all of the information you may need. There are two parameters that give you more information: **Detailed** and **Full**. However, I never use Detailed because Full gives you all of the help information, including what Detailed returns, and Detailed does not return the information I am typically looking for, which is the full information regarding the parameters of a command.

Get-Help can also search for content in help files. If you know you need a command that will use "descending" as a parameter, you can run

```powershell
Get-Help descending
```

This will list all of the help files that the word "descending" is contained within. You may notice that there are cmdlets and a HelpFile returned.

![_config.yml]({{ site.baseurl }}/images/get-help-descending.png)

Let's get back to our need for testing whether a file exists or not. Here is our command:

```powershell
Test-Path $profile
```

This will test whether or not the PowerShell profile exists. The result from running this command is the word "True" returned to the console. If you were paying attention when you ran "Get-Help Test-Path -Full" you would have seen the Output section said it would return a "System.Boolean" type. (Another reason to use the Full parameter of Get-Help.)

What if instead of Test-Path you were using Get-Item?

```powershell
Get-Item $profile
```

The results look a bit different. You will see four properties: Mode, LastWriteTime, Length, and Name. Since it is returning information on a file, where is the creation date and time? What about the path? It is sort of there but it is not in the table style results. How can you find out all the details on the results of this command? On to the final leg of the tripod:

## Get-Member

Get-Member will help you understand the results from a cmdlet. It will give you all the properties and all the methods and all the everything related to the object you are querying. If you run the following command you will get all of the details from the Get-Item command results:

```powershell
Get-Item $profile | Get-Member
```

>**Pro Tip**: I almost always pipe into Get-Member (and because I'm about speed, I use the alias "gm" for Get-Member). You can use Get-Member's InputObject parameter to do the same thing, I just never do since only the InputObject parameter takes pipeline input for Get-Member. Also, you don't have to restructure your command to get it to work.

If you ran the above command you will see that the object returned by Get-Item has a lot more information than is displayed by default. You can see that there is a FullName property, an IsReadOnly property, etc. You can also see the type of data for the property. Note the difference between the **Directory** and the **DirectoryName** properties. One is an object type and the other is a string type. The visible output is the same between the two, but how you would interact with them in PowerShell would be different.

Get-Member also shows the methods that are available for the object. If you are familiar with .NET methods then this will be easy for you. If you are not familiar don't worry. As you continue to work with PowerShell and review examples of other people's code you will start to become familiar with how methods work. Here is a simple example using what we have worked with so far. Let's take the $PROFILE variable and turn the filename to lowercase. Remember the command to get the file object data:

```powershell
Get-Item $profile
```

Since all we want is the Name property, we will return just that property from the object:

```powershell
(Get-Item $profile).Name
```

Now we will use the Get-Member command to see what methods are available to us for the Name property:

```powershell
(Get-Item $profile).Name | Get-Member
```

Looking through the methods we see the "ToLower" method. That sounds like what we need, so we will add that method to the command that returns the Name property:

```powershell
(Get-Item $profile).Name.ToLower()
```

Bingo! That is exactly what we were wanting. Looking at the other methods may give you some ideas about what else could be done to the Name property. Since the Name property is a String type, all of these methods are available for all string types. The key take away is the Get-Member cmdlet exposes the object type and what can be done with the object and what all the properties are and what type each property is. That is some powerful information.

---

## Summary

Get familiar with the tripod of Get-Command, Get-Help, and Get-Member. They are powerful and useful cmdlets that you can use to expand your understanding of how to effectively use PowerShell to accomplish your work and become a more capable and more valuable professional.