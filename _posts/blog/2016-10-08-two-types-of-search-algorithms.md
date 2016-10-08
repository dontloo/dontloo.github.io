---
layout: post
title: "Two Types of Search Algorithms"
modified:
categories: blog
excerpt:
tags: []
date: 2016-10-08
modified: 2016-10-08
---

##Basics

There're two types of search algorithms, tree based and hash based.
Perhaps the simplest applications of the two are [`tree maps`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) and [`hash maps`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html).

The performance of hash based search relies largely on the choice of hash functions, which are often to be desinged carefully for different cases. Why not always using tree based search then? The limitation of tree based search is it requires the elements to be **comparable**, which means a valid [metric](https://en.wikipedia.org/wiki/Metric_(mathematics)) needs to be defined across the elements.

##Approximate Nearest Neighbors
Serch \\( k \\) nearest
serch within radius
priority queue.
```ruby
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
```
Here is an example MathJax inline rendering \\( 1/x^{2} \\), and here is a block rendering: 
\\[ \frac{1}{n^{2}} \\]
