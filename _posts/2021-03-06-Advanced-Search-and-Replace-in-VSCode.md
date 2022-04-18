---
layout: post
title: Advanced Search and Replace in VSCode 
---

Sometimes, you are copying a document you wrote in [favorite editor] as text, but now you want to post it as a markdown document. I know, I know. Converting to markdown happens to me _all_ the time! Luckily, there is a tip I'd like to share to help you with some of the markdown elements.

Let's say you have the following content in your document (see my post [RegEx Engines Are Not the Same](https://blog.stevenjudd.com/RegEx-Engines-Are-Not-The-Same/)):

![_config.yml]({{ site.baseurl }}/images/Advanced-Search-and-Replace-in-VSCode-1.png)

What you want to do is replace all the URL links with proper markdown formatting. This is not a big deal if you have a couple of links. But what if you have many links in your document? It would be much easier to do a search and replace. But how can you use search and replace when each link is unique?

**VSCode** and **Regular Expressions** to the rescue!

## Part 1: Searching

The first thing you need is to open Find and Replace on VSCode. I use Ctrl+H because it is fast and somewhat ubiquitous for apps with a find and replace feature. If you like the menu method, click on Edit, then Replace.

Next, you need to specify that you want to use a Regular Expression. Either click the ```.*``` in the Find box or press Alt+R to specify RegEx search. Make sure you don't have the Match Case option (```Aa```) specified. Matching all the cases would be hard, and the goal is to make your life easy. 😉

Now it is time to build the RegEx that will find all of your URLs and make sure and get the correct characters so it works properly. It is at this point where people somewhat new to RegEx get intimidated or frustrated. Don't worry. You will get better when you spend more time using it.

Start with the ```http``` part of the URL. Note that in the content example, there are URLs with ```http``` and ```https```. You will need an expression that gets both. That means you will start with ```http``` since that is in both formats. This will be followed by ```s?``` which means zero or one ```s``` character. Then the search will need to get the colon and two slashes, so you will add ```://``` to the search. VSCode will help by highlighting the text that matches, like this:

![_config.yml]({{ site.baseurl }}/images/Advanced-Search-and-Replace-in-VSCode-2.png)

> **Note:** if you enter this pattern into [https://regex101.com](https://regex101.com), it will note that "An unescaped delimiter (/) must be escaped with a backslash." VSCode does not error with these being unescaped, but regex101 will. Adding the escape characters will not break the search for VSCode.

Now it gets a bit tricky. You want to get the rest of the URL but not get any extra characters. This is usually a trial and error process. You can do some searches for examples, but the results you find may be for some specification-compliant URL testing. Your URLs may not be that complicated, and you don't want to have to slog your way through a RegEx string that looks like this (especially if it doesn't work):

```((http|https)://)(www.)?[a-zA-Z0-9@:%._\\+~#?&//=]{2,256}\\.[a-z]{2,6}\\b([-a-zA-Z0-9@:%._\\+~#?&//=]*)```

The above example is from [https://www.geeksforgeeks.org/check-if-an-url-is-valid-or-not-using-regular-expression/](https://www.geeksforgeeks.org/check-if-an-url-is-valid-or-not-using-regular-expression/)

In this case, you know that all the URLs have either a space, a comma, or an EOL (end of line) character after the URL text. So after the ```://``` in the Find box, you add ```.*?``` to get all characters up to the next found item, which would be ```( |,|$)```, which represents space or comma or EOL. Now you can see that all the URLs in the text are highlighted properly. Part 1 is complete. You can search and find all the URLs.

## Part 2: Replacing

Next is the replacement syntax. You will want to convert the URL text to the following markdown format:

```[URL](URL)```

In other words, if the URL was stored in a variable named ```$URL```, you would use ```[$URL]($URL)``` as your replacement.

You will use a RegEx capture group to put what was found by the search string back into the replacement. In RegEx, text inside parenthesis is a group construct. One of the construct types is a capture group. When you have capture groups, RegEx will create matches for the text that matches the pattern specified. The matches follow the capture groups and are numbered from left to right, unless you use a named capture group or a non-capturing group. Simple, right? Maybe not. [Here is some documentation](https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference#grouping-constructs) if you really want to learn about group constructs.

Again, since the goal is to keep this simple, you will use ```(https?://.*?)( |,|$)``` as the RegEx search string. Note the addition of another set of parenthesis. Also note that there is a space before the first pipe character. There are now two capture groups in the search string.

Finally, you need to enter the desired output into the Replace box. A dollar sign precedes a capture group variable. Thus, you would use ```[$1]($1)``` as your Replace string. Unfortunately, there is no easy way to test the replacement other than to run it. Just be ready to Ctrl+Z if you don't get the desired output.

> **Note:** you may need to use curly braces after the dollar sign if you need to add numeric values directly after the group or if you are using named capture groups. As an example, if you used ```(?<url>https?://.*?)(?: |,|$)``` as your Find string then you would use ```[${url}](${url})``` as your Replace string.

Speaking of Ctrl+Z, if you run the above replacement, it will mess up the output. I could have corrected this and left this part out of the post, but I wanted to show that sometimes you may overlook something or don't anticipate the results. It can happen to all of us. What I forgot was to add back in the second capture group. Thus, it was stripping off the space, comma, or EOL characters. To fix this, add ```$2``` to the end of the Replace string. Here is what the Find and Replace box looks like:

![_config.yml]({{ site.baseurl }}/images/Advanced-Search-and-Replace-in-VSCode-3.png)

Using the replace text ```[$1]($1)$2``` shows that it works as expected, with one notable exception. If you already have a URL in the proper markdown format, the RegEx shows it as a match. Thus, you cannot do a Replace All, as that would wreak some havoc on those URLs in proper markdown format. You _could_ modify the RegEx to exclude any matches that start with a left square brace or a left parenthesis. That match would need to use negative lookbehinds, something I will not cover this time, but the search text would be ```((?<!\[)(?<!\()https?:\/\/.*?)( |,|$)``` including the escaped slashes after the colon. You should be able to do a Replace All with this RegEx string as your Find value.

I hope this helps you understand how to use a Regular Expression to find what you are looking for and capture group variables as part of a dynamic replacement.

