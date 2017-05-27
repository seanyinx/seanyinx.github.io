---
layout: post
title: Stats Calculator with TDD Part 2
date: 2016-12-31 16:27:13 +0800
categories: TDD
tags: [TDD, XP, Testing]
---
We implemented finding minimum value from a sequence of integers. Finding maximum and average is very straightforward and similar to what we have done in my previous post. So I will just put the code here directly to keep us from being bored.

<!-- more -->

## Test Cases
If you try with the sample integer sequence in my previous post, you may find that the calculated average is different from the expected one. I believe it's a mistake in the original Kata.
```java
public class StatsCalculatorTest {

    private StatsCalculator statsCalculator = new StatsCalculator();

    @Test
    public void minOfSomeElementsReturnsTheMinimum() {
        int min = statsCalculator.minOf(6, 9, 15, -2, 92, 11);

        assertThat(min, is(-2));
    }

    @Test
    public void minOfBlowsUpWhenNoElementProvided() {
        try {
            statsCalculator.minOf();
            Assert.fail(IllegalArgumentException.class.getName() + " expected");
        } catch (IllegalArgumentException e) {
            assertThat(e.getMessage(), is("No element provided"));
        }

    }

    @Test
    public void maxOfSomeElementsReturnsTheMinimum() {
        int max = statsCalculator.maxOf(6, 9, 15, -2, 92, 11);

        assertThat(max, is(92));
    }

    @Test
    public void maxOfBlowsUpWhenNoElementProvided() {
        try {
            statsCalculator.maxOf();
            Assert.fail(IllegalArgumentException.class.getName() + " expected");
        } catch (IllegalArgumentException e) {
            assertThat(e.getMessage(), is("No element provided"));
        }

    }

    @Test
    public void averageOfSomeElementsReturnsTheMinimum() {
        double average = statsCalculator.averageOf(6, 9, 15, -2, 92, 11);

        assertThat(average, closeTo(21.833333, 0.00001));
    }

    @Test
    public void averageOfBlowsUpWhenNoElementProvided() {
        try {
            statsCalculator.averageOf();
            Assert.fail(IllegalArgumentException.class.getName() + " expected");
        } catch (IllegalArgumentException e) {
            assertThat(e.getMessage(), is("No element provided"));
        }

    }
}
```

## Product Code
The production code for finding minimum, maximum, and average values looks like the follows.
```java
public class StatsCalculator {
    public int minOf(int... elements) {
        if (elements.length == 0) {
            throw new IllegalArgumentException("No element provided");
        }
        int min = Integer.MAX_VALUE;
        for (int element : elements) {
            min = Math.min(element, min);
        }
        return min;
    }

    public int maxOf(int... elements) {
        if (elements.length == 0) {
            throw new IllegalArgumentException("No element provided");
        }
        int max = Integer.MIN_VALUE;
        for (int element : elements) {
            max = Math.max(element, max);
        }
        return max;
    }

    public double averageOf(int... elements) {
        if (elements.length == 0) {
            throw new IllegalArgumentException("No element provided");
        }
        int sum = 0;
        for (int element : elements) {
            sum = element + sum;
        }

        return ((double) sum) / elements.length;
    }
}
```
Are we done? There are quite a few duplicate code in the implementation above, such as the exception handling and looping of elements.

## Refactoring
It seems the only differences among the three methods are the initial min/max/sum value and operation on each element. We can extract the duplicate code to a common method, if we can pass those two as parameters.
 
The only way to pass operations by parameter is to encapsulate the operations in objects and pass the objects as a parameter. In order for a single method to accept different types of operations, the objects containing the operations have to implement a common interface.

### 1. Extracting operations
We have first extract min/max/average operations into objects.

* Extracting min operation

{% include video.html url="/assets/tdd/07.swf" %}

* Extracting max operation

{% include video.html url="/assets/tdd/08.swf" %}

* Extracting average operation

{% include video.html url="/assets/tdd/09.swf" %}

### 2.Extracting common interface
 
{% include video.html url="/assets/tdd/10.swf" %}

### 3. Extracting duplicate code to a method
With operations extracted to objects implementing the same interface, we are ready to extract duplicate code to a common method and pass both initial value and operation of min/max/average to the method by parameter.

{% include video.html url="/assets/tdd/11.swf" %}

## The Final Code
We have finished refactoring our code and we shall run the test cases again (multiple times during the refactoring as well) to make sure everything is fine.

* Operation Interface
```java
public interface Command {
    int invoke(int element, int aggregate);
}
```

* Stats Calculator
```java
public class StatsCalculator {

    private final Command minCommand = new MinCommand();
    private final Command maxCommand = new MaxCommand();
    private final Command averageCommand = new AverageCommand();

    public int minOf(int... elements) {
        return aggregate(Integer.MAX_VALUE, minCommand, elements);
    }

    public int maxOf(int... elements) {
        return aggregate(Integer.MIN_VALUE, maxCommand, elements);
    }

    public double averageOf(int... elements) {
        int sum = aggregate(0, averageCommand, elements);

        return ((double) sum) / elements.length;
    }

    private int aggregate(int value, Command command, int[] elements) {
        if (elements.length == 0) {
            throw new IllegalArgumentException("No element provided");
        }
        int result = value;
        for (int element : elements) {
            result = command.invoke(element, result);
        }
        return result;
    }

    private static class MinCommand implements Command {

        @Override
        public int invoke(int element, int min) {
            return Math.min(element, min);
        }
    }

    private static class MaxCommand implements Command {

        public int invoke(int element, int max) {
            return Math.max(element, max);
        }
    }

    private static class AverageCommand implements Command {

        public int invoke(int element, int sum) {
            return element + sum;
        }
    }
}
```

## Summary
We have eliminated duplicate code and made our production code much easier to read. Moreover, if there's a new requirement asking to perform more calculations, such as variance of elements, we are able to achieve that easily by implementing another subclass of `Command` interface.
 
If you look at our test cases, they are concrete and quite easy to understand. I am pretty sure we achieved 100% test coverage too.

To me, another benefit of TDD is fun. I am achieving all the benefits mentioned in my previous post while having fun! It will be totally different but terrible experience to write test cases after completing production code. If you don't believe me, try it yourself.
