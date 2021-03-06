---
layout: post
title: RegEx Engines Are Not the Same
---

In case you ever run across a situation where you are using RegEx and are getting unexpected results, you need to know that RegEx engines are not all the same. PowerShell uses the .NET engine, which should not come as a surprise since PowerShell runs on .NET.

I like to use [https://regex101.com](https://regex101.com) to test my RegEx patterns because I like the explanation tree and the help examples. Also, it has a selectable engine (Flavor) to choose how it will interpret the pattern. Unfortunately, .NET is not one of the options. [https://regexr.com/](https://regexr.com/) is another popular site to test expressions, but I still like regex101 better, and regexr doesn't use the .NET engine either. Thus, you can use [http://regexstorm.net/tester](http://regexstorm.net/tester), which does use the .NET engine.

If you go down the engine rabbit hole, you will find other options and terms, like PCRE, PCRE2, RE2, and more. Good luck in there! I hope you find your way back. 😉

Finally, there are some good visualizers, if you are more of a visual learner. Here are few options:

[https://www.debuggex.com](https://www.debuggex.com) is a fun site that will allow you to debug your expression while building a visualization for you.

[https://blog.robertelder.org/regular-expression-visualizer](https://blog.robertelder.org/regular-expression-visualizer) is another visualization site, but it is much more detailed and will help you learn how RegEx functions.

If you want your explanation in your uber editing tool, VSCode, then look at the Regexp Explain extension: [https://marketplace.visualstudio.com/items?itemName=LouisWT.regexp-explain](https://marketplace.visualstudio.com/items?itemName=LouisWT.regexp-explain)

Why is knowing which engine is in use important? Subtle differences in how the engines do their matching and the features they enable may mean that your expression works in one place and not in another. For example, Go and Kusto are based on the RE2 engine. If you are testing your expression in regex101 using PCRE and it doesn't work in KQL, then the parsing engine may be the reason.

Happy RegExing!
