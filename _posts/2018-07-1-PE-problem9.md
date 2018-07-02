---
title: "Project Euler : Problem 9 - Special Pythagorean triplet"
excerpt_separator: "<!--more-->"
categories:
  - Project Euler
tags:
  - Project Euler
  - Prime Numbers
toc: true
toc_sticky: true
---

## Problem Statement : Special Pythagorean triplet
[Problem 9](https://projecteuler.net/problem=9) : A Pythagorean triplet is a set of three natural numbers, $$a < b < c$$, for which,
{: .text-justify}

$$a^2 + b^2 = c^2$$

For example, $$3^2 + 4^2 = 9 + 16 = 25 = 5^2$$.

There exists exactly one Pythagorean triplet for which $$a + b + c = 1000$$. Find the product $$abc$$.
{: .text-justify}

## Concept and Theory
First of all I want you to read about [Pythagorean triplets](/math/Article-Pythagorean-Triplet/), if you haven't.
{: .text-justify}

### Approach 1

From Pythagorus Theorem we know,
{: .text-justify}

$$a^2 + b^2 = c^2$$

and we are given to satify,
{: .text-justify}

$$a + b + c = n \ \ or \ \ c = n - a - b$$

Substituing this value in Pythagorus Theorem we will get,
{: .text-justify}

$$a^2 + b^2 = (n-a-b)^2 \\

a^2 + b^2 = n^2 +(a-b)^2 -2n(a+b) \\

a^2 + b^2 = n^2 + a^2+b^2+2ab - 2an - 2bn \\

a^2 - (a-n)^2 = b(2a-2n) \\

b = \frac{a^2-(a-n)^2}{2(a-n)} \\

b = \frac{(n)(2a-n)}{2(a-n)} \\

b = \frac{(n)(n-2a)}{2(n-a)} $$

We can see that there is something odd about the above equation that is $$a \leq n$$ in denominator. But its fine as numerator will also be negative then for $$a \leq \frac{n}{2}$$.
{: .text-justify}

So, we just have to iterate over $$a$$ from $$1$$ to $$\frac{n}{2}$$ to find integral values of $$b$$.
{: .text-justify}

### Approach 1 code
```ruby
/**
 * A function for Project Euler problem 9
 *
 * @param n
 *            maximum sum of a,b and c
 *
 * @return the maximum product
 */
public static long specialPythagoreanTriplet(int n) {

  long maxProduct = -1;

  for (int a = 1; a < n / 2; a++) {
    int numerator = n * (n - 2 * a);
    int denominator = 2 * (n - a);
    if (numerator % denominator == 0) {
      int b = numerator / denominator;
      int c = n - a - b;

      long tempProduct = a * b * c;

      if (tempProduct > maxProduct) {
        maxProduct = tempProduct;
      }
    }
  }

  return maxProduct;
}
```

### Without coding
I fount this beautiful approach by a person, $$Pier$$ , on [ProjectEuler](https://projecteuler.net) exploiting on [Pythagorean triplets](/math/Article-Pythagorean-Triplet/) generation.

$$We \ knows \ from \ Euler \ Pythagorean \ Triplet \\
a= 2mn \ , \ b= m^2 -n^2 \ , \ c= m^2 + n^2 \\
We \ are \ given, \ a + b + c = 1000 \\
\implies 2mn + (m^2 -n^2) + (m^2 + n^2) = 1000 \\
\implies 2mn + 2m^2 = 1000 \\
\implies 2m(m+n) = 1000 \\
\implies m(m+n) = 500 \\
As \ m>n \\
m= 20 \ n= 5 \\
will \ give \ us \ a= 200 \ , \ b = 375 \ , \  c= 425$$


## Test Your Skills
Wanna try a harder version of the above problem ? Check this [HackerRank](https://www.hackerrank.com/contests/projecteuler/challenges/euler009) problem.
{: .text-justify}

### Solution
The solution will remain same as given in the above mentioned post, $$specialPythagoreanTriplet$$, you just need to call it for each test case.
{: .text-justify}

## References and Further Readings
* [ProjectEuler](https://projecteuler.net)
* [Wikipedia](https://en.wikipedia.org/wiki/Pythagorean_triple)
