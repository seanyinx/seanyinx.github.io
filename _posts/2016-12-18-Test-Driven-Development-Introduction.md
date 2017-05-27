---
layout: post
title: "Test Driven Development Introduction"
date: 2016-12-18 11:29:15 +0800
categories: TDD
tags: [TDD, XP, Testing]
---

## The Pain of Automated Testing
I've been writing code for a living for over a decade. I have seen some projects with **good** code
(***clear responsibilities, high cohesion, low coupling, easy to change, and pleasant to read***) and many with **bad** code
(***nobody wants to touch***).

Like marriage, good ones all look alike and bad ones are bad in different ways. One of the most important characteristics
to differentiate the good from the bad is multi-layer of **effective and automated tests**.

Most programmers know that ***[automated tests help our team work at a sustainable pace with a manageable level of technical debt](https://www.agileconnection.com/article/test-automation-project)*** (by Lisa Crispin, co-author of [Agile Testing](http://amzn.to/2qD1QfU) and [More Agile Testing](http://amzn.to/2qdwIT5)).
But why don't we exercise such an incredible practice in so many projects?

Let's answer these two questions first.

<div class="message" markdown="1">
Q: What's the purpose of testing?

A: **Verification** of code behavior meeting our expectation

Q: What's the interest of programmers?

A: **Problem solving**
</div>

We have verified the code behavior in our mind while programming and doing it again in test cases is just another repetition,
which we are not interested in! If given any excuse, we will happily skip this part.

How do we make ourselves **love** writing automated tests? My answer is **Test Driven Development** (**TDD**).

**TDD** is one of the eXtreme Programming (XP) practices developed by Kent Beck (author of [Test Driven Development: By Example](http://amzn.to/2qf61Og)).
It promotes repetitions of short coding cycles, to evolve the solutions with new requirements.

<!-- more -->

## The Coding Cycle of TDD
TDD has a "mantra" with 3 steps, *red/green/refactor*:
* Write a simplest failing test case (hence **<span style="color:red">red</span>**), before writing any production code.
* Write minimal production code possible to pass the failing test case (**<span style="color:green">green</span>**)
* **<span style="color:blue">Refactor</span>** test case or production code

This coding cycle is repeated for every scenario of requirements.

{% include image.html
            img="/img/tdd.mantra.png"
            title="TDD Mantra" %}

So how does TDD answer the question of programmers not liking to write automated tests? By writing a test case first before
any production code, we force ourselves to design a single scenario how our production code will be used. It's like
creating a cake mold first.

{% include image.html
            img="/img/Hello.Kitty.cake.mold.jpg"
            title="Hello Kitty cake mold"
            caption="[Creative Commons Hello Kitty cake mold](https://www.flickr.com/photos/annettepedrosian/2899723301/) by [Annette Young](https://www.flickr.com/photos/annettepedrosian/) is licensed under [CC BY 2.0](https://creativecommons.org/licenses/by-nc-nd/2.0/)" %}
            
The test case guarantees that our production code written meets the expectation under the scenario. Nothing more and nothing less,
if we follow the rules above of writing minimal production code to pass the failing test case only, just like baking a
cake with the mold above.

{% include image.html
            img="/img/Hello.Kitty.cake.jpg"
            title="Hello Kitty cake"
            caption="[Creative Commons Hello Kitty Strawberry Birthday Cake](https://www.flickr.com/photos/karenchen/17490321018/in/photolist-sDyt5W-qs8idg-pviX2L-qsig7M-pviTas-qaRHhV-jg1VDn-fnEVco-fnEV6C-eBKMyB-ejixp4-dTU1pN-dBHct7-dq7kHz-dcFCNZ-d7ZGB7-d7vHWf-bTyQja-bLy3Ai-bspp18-9MTiyu-9DYMco-9CzK7X-9Aisnr-9ewpdb-9cn8wD-9cn8ig-9cn7Zn-8Vyetw-8QPhek-8vaR2f-8jtnxy-85n4UD-7inaLP-7inaKk-7foaQ1-6Sk9ZC-67fBxT-5U2tgD-5vQAge-5vUUCq-5vUUyW-5qeQLe-5oaRWJ-5ahDUm-4Y7arT-4vc6Pe-KtJNn-KpnLY-zFkNU) by [Karen](https://www.flickr.com/photos/karenchen/) is licensed under [CC BY 2.0](https://creativecommons.org/licenses/by-nc-nd/2.0/)" %}

What if we write test cases after production code? Well, we may get something close to our expectation, over design our logic, or even slip some boundary cases.

{% include image.html
            img="/img/Hello.Kitty.cake.cropped.jpg"
            title="Hello Kitty cake"
            caption="[Creative Commons Hello Kitty cake for Lydia's fifth birthday](https://www.flickr.com/photos/anthonares/6997709930/) by [Anthony Kendall](https://www.flickr.com/photos/anthonares/) is licensed under [CC BY 2.0](https://creativecommons.org/licenses/by-nc-nd/2.0/) / Cropped from original" %}

Writing test cases afterwards is like wrapping a baked cake with a cake box. We are happy as long as the cake box is large enough 
and it may be much bigger than what's specified in our requirements. The fun of test design is lost.

## The Benefit of TDD
### Better design
As we know, tightly coupled code are hard to test. Since we always write tests before any production code, our code are always testable, 
meaning it is hard to write tightly coupled code with TDD.

### Much less code debugging
We are working in short cycles of **<span style="color:red">red</span>/<span style="color:green">green</span>/<span style="color:blue">refactor</span>** with TDD. There won't be much code written after the previous time our tests passed.
That limits the scope of the bug we introduced and makes it very easy to spot.

### No fear to break code
TDD tends to produce code with very high test coverage (90%+ is very easy to achieve), since tests are always written first.
It's much less likely to break the code accidentally with such high code coverage.

### Test case as documentation
If written well, test cases are the best documentation, because they are always up to date and describe the exact scenarios on how to use the production code.

## How To Start?
TDD is an easy-to-learn but hard-to-master skill. The best way to improve our skill on TDD is through practices.
There are many exercises called [*Kata*s](https://github.com/garora/TDD-Katas), which can help accelerate our learning process.
I will use one of the simplest Kata, [Calc Stats](https://github.com/garora/TDD-Katas#calc-stats) to demonstrate how to get started with TDD in my next post.
