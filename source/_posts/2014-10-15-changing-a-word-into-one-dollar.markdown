---
layout: post
title: "Capturing Regexp and Using '$1'"
date: 2014-10-15 19:46:06 -0400
comments: true
categories: Flatiron School
---

####Premise
Last night I was solving a problem on [CodeWars](www.codewars.com) and though I solved it, I came across a solution I found much cooler and decided to write this post about it. The solution used a regular expression with a capture and this funny little character '$1' which made me want to find out exactly what was going on so I could use it in the future.


###Relevant Regexp Information

####Capturing vs. Matching
In regular expressions you can either match or capture an item. Matching a string is merely a 'yes' or 'no' statement where the string either has a match or doesn't and it returns nothing. On the otherhand, capturing takes the matching item and returns that match so you can infact use that match for some other purpose.
{% img /images/match.png %}
Match example
{% img /images/capture.png %}
Capture example

As you can see in the [Rubular](www.rubular.com) match example, it simply matches the substring. However, in the capture example there is a section 'Match groups', which represents the match which was saved in memory for further use.

####What is this '$1'?

The '$1' is an example of some special global variables withing a ruby RegExp expression. According to the ruby regexp documentation pattern <strong><u>matching</u></strong> sets some global variables

* $~ is equivalent to ::last_match;
* $` contains string before match;
* $' contains string after match;
* $1, $2 and so on contain text matching first, second, etc capture group;
* $+ contains last capture group.

####Tying it together
So back to the CodeWars problem....this is what was asked.
>We need a method for parsing an array of strings to see which of 3 categories they fall into:

##### Rules
  1. :alpha strings contain the word "alpha"
  2. :beta strings contain the word "beta"
  3. :unknown strings don't contain either "alpha" or "beta"
  4. :unknown is also used for nil entries
  5. No string will contain both "alpha" and "beta"
  6. The strings can contain alpha and beta in any case (e.g. "Alpha", "BeTa")

```ruby
lines = ["This is an alpha line", "Beta line next!", "Another AlphA", "I have no idea", nil]
#=> example input

line_types(lines)
#=>  [ :alpha, :beta, :alpha, :unknown, :unknown ] example output

```
##### ORIGINAL SOLUTION
```ruby
def line_types lines
  lines.collect do |line|
    if line =~ /alpha/i
      :alpha
    elsif line =~ /beta/i
      :beta
    else
      :unknown
    end
  end
end
#=>  [ :alpha, :beta, :alpha, :unknown, :unknown ]
```

##### NEW SOLUTION
```ruby
def line_types lines
  lines.collect { |line| line =~ /(alpha|beta)/i ? $1.downcase.to_sym : :unknown }
end
#=>  [ :alpha, :beta, :alpha, :unknown, :unknown ]
```

####Summary
While my original solution works perfectly fine, the new solution uses some cooler ruby (in my opinion) by implementing everythign on one line. The method takes an array of lines and runs the .collect method on it. Each 'line' is tested against the regexp /(alpha|beta)/i which is looking for either a alpha substring OR beta substring with the 'i' meaning case-insensitive. Then if this match is found, since it is in capture parenthesis, the matched string is saved and can be accessed by the '$1' variable. Then all that is down is downcasing and turning it into a symbol as per the rules. If nothing is matched then the :unknown symbol is placed in the return array. Pretty cool stuff.

#####Resources
* (http://stackoverflow.com/questions/21200514/regular-expression-matching-vs-capturing)
* (http://www.ruby-doc.org/core-2.1.1/Regexp.html)
* (http://stackoverflow.com/questions/288573/1-and-1-in-ruby)