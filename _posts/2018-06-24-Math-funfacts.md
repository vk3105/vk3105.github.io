---
title: "Fun Facts and General Concepts"
excerpt_separator: "<!--more-->"
categories:
  - Math
tags:
  - Trailing Zeroes in Factorial
  - Highest Power in Factorial
  - FunFacts
toc: true
toc_sticky: true

---

**This page is dedicated to some of the day to day life normal math stuff. I will keep updating this page to my heart's content. Haha !!!**
{: .text-justify}

**I will highly recommend you to use the table of contents, shown on right side, to browse the topics. This post will be too long**
{: .notice--info}

## Highest power of number in a factorial

### An Example and Little Theory
Lets say we have a given number's, $$N$$ factorial and we are asked to find the highest power of say another number $$a$$. How we will do it?
{: .text-justify}

For example $$N=20$$ and $$a=2$$.
{: .text-justify}

$$N!=20! = 1 \times 2 \times 3 \times \dots 20$$
{: .text-justify}

A manual testing for $$n=20$$ will give us the following result,
{: .text-justify}

$$Total \ 2's \ in \ 20! \ = \ 18$$
{: .text-justify}

The next question arises is from where we will get $$2's$$? We can get $$2$$ from all the multiples of $$2$$.
Hmm... so can we say the quotient of $$20/2 = 10$$ will give us what will be the highest power of $$2$$ ? Yes its partially correct, but have you considered these cases,
{: .text-justify}

$$4 \ = \ 2^2 \\
8 \ = \ 2^3 \\
16 \ = \ 2^4 $$
{: .text-justify}

If you have missed these numbers you didn't considered few powers of $$2$$ which should be counted. Thus, our next step will be to consider them too.
{: .text-justify}

$$4 \ = \ 2^2 \ (gives \ 1 \ extra \ 2)\\
8 \ = \ 2^3 \ (gives \ 2 \ extra \ 2)\\
16 \ = \ 2^4 \ (gives \ 3 \ extra \ 2) \\
Total \ 2's \ = \ (20/2) + 1 + 2 + 3 = 16$$
{: .text-justify}

We are still short by $$2$$ twos. You will but your brain into action and see the manual calculations and finds out you haven't considered following numbers,
{: .text-justify}

$$12 \ = \ 2^2 \times 3  \ (gives \ 1 \ extra \ 2) \\
20 \ = \ 2^3 \times 5 \ (gives \ 1 \ extra \ 2) \\
Total \ 2's \ = \ (20/2) + 1 + 2 + 3 +1 +1 = 18$$
{: .text-justify}

### Theory
From the above example we saw,
{: .text-justify}

$$ All \ multiples \ of \ 2 \ will \ give \ us \ 1 \ 2 \\
All \ the \ multiples \ of \ 4 \ will \ give \ us \ 1 \ extra \ 2 \\
All \ the \ multiples \ of \ 8 \ will \ give \ us \ 2 \ extra \ 2 \\
All \ the \ multiples \ of \ 16 \ will \ give \ us \ 3 \ extra \ 2 \\
\dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots\\
\dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots \dots\\
All \ the \ multiples \ of \ 2^n \ will \ give \ us \ n-1 \ extra \ 2 $$

### Formula 1
Above observations leads to one thing only, count how many multiples are there for each power of $$a$$ in given factorial $$N!$$, till the multiples for a particular power becomes $$0$$.
{: .text-justify}

$$Highest \ power \ of \ a \ in \ N! \\
= \Bigg \lfloor{\frac{N}{a^1}} \Bigg \rfloor+\Bigg \lfloor{\frac{N}{a^2}} \Bigg \rfloor+\Bigg \lfloor{\frac{N}{a^3}} \Bigg \rfloor+\Bigg \lfloor{\frac{N}{a^4}} \Bigg \rfloor + \dots \dots $$

Testing in our above sample example

$$Highest \ power \ of \ 2 \ in \ 20! \\
= \Bigg \lfloor{\frac{20}{2^1}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{2^2}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{2^3}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{2^4}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{2^5}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{2^6}} \Bigg \rfloor + \dots \dots  \\
= \Bigg \lfloor{\frac{20}{2}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{4}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{8}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{16}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{32}} \Bigg \rfloor+\Bigg \lfloor{\frac{20}{64}} \Bigg \rfloor + \dots \dots $$
$$= 10 + 5 + 2 + 1 + 0 + 0 \dots \dots \\
= 18 (As \ expected.)$$

### Formula 2 : Neat trick
Well there is another very simple way of doing this and saving our-self from powers minefield.
{: .text-justify}

**We just have to repeatedly divide quotient by $$a$$ till we get $$0$$ as quotient. Add all the quotients, that will be our answer.**
{: .text-justify}

For Eg: $$N=20 \ and \ a = 2$$

$$20/2 = 10$$

$$10/2 = 5$$

$$5/2 = 2$$

$$2/2 = 1$$

$$1/2 = 0$$

$$ Total \ sum \ of \ quotients = 10 + 5 + 2 + 1 \\
= 18$$

### Code
```ruby
/**
 * A function to calculate the highest power of a number "a" in N!
 *
 * @param num
 *            the factorial number
 * @param a
 *            the number whose highest power needs to be calculated
 *
 * @return the highest power of "a" in N!
 */
public static long highestPowerInFactorial(long num, long a) {
  long quotientSum = 0;

  while (num != 0) {
    num /= a;
    quotientSum += num;
  }

  return quotientSum;
}
```
### Complexity
For a given factorial $$N!$$ and number $$a$$, complexity = $$O(log(a))$$. Because we are always reducing the size by $$a$$ in every step.
{: .text-justify}

## Find the maximum power of a number below a factorial
The question is find the maximum value of $$b$$ for a given $$a$$ in $$N!$$ for which $$a^b <= N!$$
{: .text-justify}

I will just write the code. Its a simple problem.
{: .text-justify}

### Code
```ruby
/**
 * A function to calculate the Maximum Power Of a Number In Factorial
 *
 * @param num
 *            the factorial number
 * @param a
 *            the number whose highest power needs to be calculated
 *
 * @return the maximum power of number in Factorial
 */
public static long maximumPoweredValueOfNumberInFactorial(long num, long a) {

  long maxPower = 0;
  long currentNumber = a;
  while (num > currentNumber) {
    currentNumber *= a;
    maxPower++;
  }

  return maxPower;
}
```

## Number of zeros at the end of a factorial
How to find the number of trailing zeroes in a given factorial?
{: .text-justify}

### Theory
Well to make a $$10$$ we need one $$2$$ and one $$5$$ and that will make a trailing zero in a factorial. That's it.
How to count how many $$2's$$ and $$5's$$ are there ? Basically we need to know whats the highest power of $$2$$ and $$5$$ are there in $$N!$$. We discussed this in above subsection([Here](#highest-power-of-number-in-a-factorial)).
{: .text-justify}

Lets say,

$$ x \ = \ highest \ power \ of \ 2 \ in \ N! \ and, $$
$$ y \ = \ highest \ power \ of \ 5 \ in \ N!$$
$$ {Number \ of \\ trailing \ Zeroes} =
  \begin{cases}
    x       & \quad x < y \ or \ x = y \\
    y  & \quad y > x
  \end{cases}
$$

Since we know that every alternate number is an even number so it will donate one $$2$$ at least and every $$5th$$ number will be a multiple of $$5$$. It implies that the power of $$5$$ will always be less that power of $$2$$, thus simply returning the highest power of $$5$$ in a given factorial $$N!$$ is enough.
{: .text-justify}

### Code
```ruby
/**
 * A function to calculate the trailing zeroes in a factorial num
 *
 * @param num
 *            the factorial number
 *
 * @return number of trailing zeroes
 */
public static long numberOfTrailingZeroesInAFactorial(long num) {
  return highestPowerInFactorial(num, 5);
}
```

### Complexity
For a given factorial $$N!$$, complexity = $$O(log(a))$$.
{: .text-justify}

## References
