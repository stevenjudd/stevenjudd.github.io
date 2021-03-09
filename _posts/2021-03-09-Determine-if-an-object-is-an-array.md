---
layout: post
title: Determine if an object is an array
---

There are times where you need to know if the object you are working with is an array. There is an easy way to check: use the GetType method. Try the following command:

```(Get-ChildItem).GetType()```

You can see that it has a BaseType of ```System.Array```. You can use the BaseType to see what type of object you are working with. Also, by adding the property of IsArray to the GetType method you can get a Boolean result whether an object is an array:

```(Get-ChildItem).GetType().IsArray```

Why is this important? Because different commands can return different types and you may need to code differently based on the type of result you get from a command. Adding a property to an Integer type is different than adding to a Hashtable or an Array.

Here is an excellent explanation of Arrays by Kevin Marquette if you would like to learn more: https://powershellexplained.com/2018-10-15-Powershell-arrays-Everything-you-wanted-to-know/?utm_source=blog&utm_medium=blog&utm_content=titlelink