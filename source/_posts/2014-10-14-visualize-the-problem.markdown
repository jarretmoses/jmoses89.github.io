---
layout: post
title: "Visualizing Problems and Asking the Right Questions"
date: 2014-10-14 20:05:26 -0400
comments: true
categories: Flatiron School
---

####Premise
If you're like me, you've probably gotten stuck on a problem and after awhile realized that you don't even fully understand what the problem is that you;re trying to solve. This leads to way too much time frustratingly trying to just code your way through it until something finally works. While this may be true sometimes, I've found that these next steps will help you calmly and collectively solve your problem.

  1. Stop what you're doing and take a deep breathe
  2. Ask yourself what is the current problem you are trying to solve
  3. WRITE IT DOWN
  4. Repeat until each ministep is done

####What sparked this post?
While working on the ruby-allergy lab I realized I simply did not understand how binary operators could possibly help me solve this problem. SO...I decided to ask myself how the values look in binary and I drew a picture to see if anything would click. Sure enough it did...


####What is a binary number?
A binary number is simply a representation of an integer using 1's and 0's.
Starting from the right most value (1) every next value is raised to the power of 2

|  Integer      |    Value      |
| ------------- |:-------------:| 
|      0        |        0      |
|      1        |        1      |
|      2        |       10      |
|      3        |       11      |
|      4        |      100      |
|      8        |     1000      |
|     16        |    10000      |
|               |               |

Every added digit is double the one before it

####Binary operators to know

'&' AND operator returns the common binary values between 2 numbers

```ruby
1001 
    & 
1101
#=> 1001
```

'^' XOR operator returns a value with 1 bits where either value had a 1

```ruby
0001 
    ^ 
1000
#=> 1001
```

For the purpose of this problem I only needed the '&', but including another definition of a binary operator you can get a better sense of how it works. Additionally the code snippets are not how you would actually use the operators but are setup to give maximum <strong>VISUAL</strong> understanding.


####The Problem to Solve
The problem to solve is given a allergy score, how do you figure out what allergies you have?

####Tying it all together
Now that we know the bare minimum of binary and their operators I take a look at the allergy problem. S I ask <strong>'Where does this knowledge of binary come into play within the problem?'</strong>Upon inspection I realize that each allergy's value reflected a specific binary value that fell perfectly on a power of 2.

```ruby
{"cat" => 128}
#=> 10000000 

{"Pollen" => 64}
#=> 01000000

{"Chocolate" => 32}
#=> 00100000
```

So that's all good and dandy but how does this help me solve the problem? Well quite simply the next question I asked myself is, <strong>'What does the binary score of having all allergies look like?'</strong>

```ruby
"Binary value of having ALL allergies"
#=> 11111111
```
From here the pieces start to fall into place. Each spot represents an allergy and a 1 in that spot means that you have the allergy while a 0 means you don't.Thus my minor understanding of binary is all I need becasue I've turned the problem into a graphical one rather than actully worrying about doing math in binary. The next question I asked was <strong>'How does the given allergy score look in binary?'</strong>

```ruby
"Score of 509"
#=> 0111111101
```
Looking at the binary value I realize that the value is way more than the maximum value of having all allergies. I know the answer is staring me in the face and I don't need to do any kind of complicated math. After writing this all out it hits me. If the '&' operator returns only values that have 1's in the same spot and I know both the binary scores of the one given and each allergy I can simply compare the given score with each allergy score and if anything greater than 0 returns then the allergy is added.

```ruby
"Comparing 509(given) with 128(cats)"
0111111101
          &
0010000000

#=> 10000000 Cat allergy is in the solution 

"Comparing 509(given) with 2(peanuts)"
0111111101
          &
0000000010

#=> 00000000 Peanut allergy is not in the solution     
```
The only final thing to point out is since the given score of 509 contains more binary values, the score of 128 is the equivalent of having 0 for every other value after that thus the 2 extra 0's after the 128th bit. Adding these zeros help with <strong>VISUAL</strong> clarity.


####FINAL SOLUTION

```ruby
#constant hash
ALLERGIES =  { 
                "cats" => 128, "pollen" => 64, "chocolate" => 32,
                "tomatoes" => 16, "strawberries" => 8, "shellfish" => 4,
                "peanuts" => 2, "eggs" => 1
              }

#find_allergies method
def find_allergies
  ALLERGIES.each do |allergy, value|
    if score & value > 0
      allergies << allergy
    end
  end
end
```

####SUMMARY
We as humans are visual creatures. Sometimes thinking isnt enough and the simple act of writing things down and asking questions about what you've written down is all you need to solve a problem. So next time you're stuck, draw a picture, not only can it help you but it's fun!


