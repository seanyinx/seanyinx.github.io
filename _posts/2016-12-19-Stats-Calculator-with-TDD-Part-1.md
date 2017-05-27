---
layout: post
title: Stats Calculator with TDD Part 1
date: 2016-12-19 23:19:42 +0800
categories: TDD
tags: [TDD, XP, Testing]
---

I am going to demonstrate how to complete Stats Calculator with Test Driven Development.
Before we start, let me introduce you the [three laws of TDD](http://programmer.97things.oreilly.com/wiki/index.php/The_Three_Laws_of_Test-Driven_Development) by [Robert Martin](https://en.wikipedia.org/wiki/Robert_Cecil_Martin).
1. You can't write any production code until you have first written a failing unit test.
2. You can't write more of a unit test than is sufficient to fail, and not compiling is failing.
3. You can't write more production code than is sufficient to pass the currently failing unit test.

It reads unnatural at first, but I hope you will understand better after reading this post.

<!-- more -->

## Stats Calculator
The details of this kata can be found in the link: [Calc Stats](https://github.com/garora/TDD-Katas#calc-stats).
```
Calc Stats:

Your task is to process a sequence of integer numbers
to determine the following statistics:

o) minimum value
o) maximum value
o) number of elements in the sequence
o) average value

For example: 6, 9, 15, -2, 92, 11

o) minimum value = -2
o) maximum value = 92
o) number of elements in the sequence = 6
o) average value = 18.166666
```
Let's start with finding the minimum value.

### 1. Write the 1st Failing Test
It's recommended to write the 1st failing test as simple as possible and only partially cover the requirement, since we have no production code to start with. In our case, the simplest case is to find the minimum from a single element.

Run the failing test case before proceeding with production code, in order to make sure it is effective.
{% include video.html url="/assets/tdd/01.swf" %}

### 2. Make the Test Pass
At this moment, our goal is just to make the 1st test case pass. We may have a rough design concept in mind, but we do not just put the entire design to code, since we are not sure if it's a good one.
{% include video.html url="/assets/tdd/02.swf" %}

One of the most important practices in Agile is [Simple Design](https://www.agilealliance.org/glossary/simple-design/). It's better to evolve our code gradually by writing the minimum code that make the test cases pass. Let the final solution emerge.

### 3. Write a More General Failing Test
Now we can expand our tests to cover more general cases.
{% include video.html url="/assets/tdd/03.swf" %}

### 4. Satisfy The Requirement
{% include video.html url="/assets/tdd/04.swf" %}

### 5. Write a Boundary Test Case
The happy path works fine now, but we have to take care of the boundary case, an empty sequence of integers. There's nothing much we can do except throwing an exception to tell the caller that something is wrong in this case.
{% include video.html url="/assets/tdd/05.swf" %}

By the way, it's a good practice to make sure the exception message is meaningful too, so that the issue can be easily identified in integration tests or logs in production by our support.  

### 6. Implement the Boundary Case
{% include video.html url="/assets/tdd/06.swf" %}

## Summary
Now we have seen how we can use TDD to not only fulfill the requirement, but also evolve our solution to a good design.

A very important lesson here is to start with the simplest test case possible, and gradually improve our code to a better design. It's very easy to get stuck trying to come up with a perfect solution in the first place.

We only completed finding the minimum of a sequence of integers today. Next, we will proceed with the rest of the requirements.
