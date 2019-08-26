# CodeWars Write-Ups by apmarshall

![apmarshall profile badge](https://www.codewars.com/users/apmarshall/badges/micro)

Contained in this repository are write-ups of problems worked on [CodeWars](https://www.codewars.com). 

A few notes about what you'll find here:

First, I am using CodeWars as a way of practicing the style of "Systematic Program Design" as taught by Gregor Kiczales (University of British Colombia, see the [How to Code MOOCS](https://www.edx.org/course/how-code-simple-data-ubcx-htc1x)) and the authors of [How to Design Programs](https://www.amazon.com/dp/0262534800/ref=cm_sw_r_cp_tai_f9dzDbYDKAPQN), Stephen Bloch, John Clements, Matthias Felleisen, et al. There approach has several key features:
- As described, it is systematic. This means it has a consistent process, starting with domain analysis, moving through data design, and concluding with systematically "templating" and then filling in a function.
- It tends to emphasize functional languages and recursive programming.

This latter point in particular does not always translate well into object-oriented languages like JavaScript or PHP. Though object-oriented languages often can support recursion (JavaScript seemingly being an exception), they are often not very good at it (tending to be quickly overwhelmed by the memory requirements, for example). So I will tend to (a) work out the recursive form of the program in pseudo-code, (b) demonstrate what this would theoretically look like in the given language, and then (c) translate that recursive pattern into something using a more standard for/while loop control flow for the actual solution presented.

Second, I will be working with the following languages:
- Psuedocode
- Python
- PHP
- JavaScript
- TypeScript
- Shell
- SQL

I'm also working on learning Haskell, which will eventually get introduced to these write-ups as well.

Obviously not every language is supported in every problem on CodeWars, so the write-ups will only contain the languages that are relevant to a given problem. SQL and Shell in particular are much less common, and PHP and TypeScript are moderately less common. Virtually all of these write-ups will contain Python and JavaScript.

Third, the beauty of the systematic approach I'm following here is that it creates easily understandable, easily maintainable code that is relatively short and sweet. That doesn't mean, however, that it will always be the "shortest" solution or the most "natural" to people who have started off learning on more control-flow oriented languages (like JavaScript). That's how I started out learning, too, and adopting this approach has been a significant change in mindset. But having learned this approach now, I find that it almost always results in a better, more "production ready" outcome, which is why I'm endeavoring to practice it as much as possible. With regards to shortness: there are plenty of "clever" one-line solutions on CodeWars to any of the problems we are going to work on here. While these are indeed clever, they are often not very readable or maintainable. Since those are priorities for me, if you're looking for the clever one-liners this probably won't be the right place.

Finally, I don't offer these solutions as a way of helping people "cheat" at CodeWars. I offer them as a way of cataloguing what I'm learning/practicing and explaining how to systematically approach different coding problems. So if you are reading this and/or using these solutions, don't do so just to copy and paste to accumulate points. Do so to read the analysis and learn.

Enjoy!