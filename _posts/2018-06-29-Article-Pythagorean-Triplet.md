---
title: "Pythagorean Triplets"
excerpt_separator: "<!--more-->"
categories:
  - Math
tags:
  - Pythagorean triplets
toc: true
toc_sticky: true
---
## Definition :
"Pythagorean triplets" are integer solutions to the Pythagorean Theorem (It states that the square of the hypotenuse (the side opposite the right angle) is equal to the sum of the squares of the other two sides).
{: .text-justify}

$$a^2 + b^2 = c^2$$

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/Rtriangle.png){: .align-center}
For a right triangle, the $$c$$ side is the hypotenuse, the side opposite to the right angle. The $$a$$ side is the shorter of the two sides adjacent to the right angle. Hence $$a < b < c$$.
{: .text-justify}

For example,

$$3^2 + 4^2 = 9 + 16 = 25 = 5^2$$

## Concept and Theory

### First Generating Formula
- Every odd number is the $$a$$ side of a Pythagorean triplet.
- The $$b$$ side of a Pythagorean triplet is simply $$(a^2 - 1) / 2$$.
- The $$c$$ side is $$b + 1$$.
{: .text-justify}

Here, $$a$$ and $$c$$ are always odd; $$b$$ is always even. These relationships hold because the difference between successive square numbers is successive odd numbers. Every odd number that is itself a square (and the square of every odd number is an odd number) thus makes for a Pythagorean triplet.
{: .text-justify}

### Euclid's formula

Euclid's formula is a fundamental formula for generating Pythagorean triples given an arbitrary pair of integers $$m$$ and $$n$$ with $$m > n > 0 \ and \ gcd(m, n) = 1$$. The formula states that the integers
{: .text-justify}

$$a = m^2-n^2$$

$$b = 2mn$$

$$c = m^2+n^2$$

form a Pythagorean triplet.

**Primitive Triplets** : If and only if $$m$$ and $$n$$ are coprime and not both odd or not both be even. Basically $$a$$, $$b$$ and $$c$$ are all coprime to each other.
{: .text-justify}

**Non Primitive Triplets** : When both $$m$$ and $$n$$ are odd or even, then $$a$$, $$b$$, and $$c$$ will be even, and the triple will not be primitive; however, dividing $$a$$, $$b$$, and $$c$$ by $$2$$ will yield a primitive triple when $$m$$ and $$n$$ are coprime and both odd.
{: .text-justify}

Putting above values in the Pythagorean Theorem we will get,

$$(m^2-n^2)^2 + (2mn)^2 = (m^2+n^2)^2$$

$$\implies m^4+n^4-2m^2n^2 + 4m^2n^2$$

$$\implies m^4+n^4+2m^2n^2$$

$$\implies (m^2+n^2)^2$$

$$\implies LHS = RHS$$

**Proof**

We know that,

$$a^2 + b^2 = c^2$$

$$\implies c^2 - a^2 = b^2$$

$$\implies (c-a)(c+a) = b^2$$

$$\implies \frac{(c+a)}{b} = \frac{b}{c-a}$$

As $$a$$, $$b$$ and $$c$$ are all coprime to each other and their fraction, $$\frac{(c+a)}{b}$$ will be rational. So if we consider,
{: .text-justify}

$$\frac{(c+a)}{b} = \frac{m}{n}$$

Then,

$$\frac{(c-a)}{b} = \frac{n}{m}$$

Solving for $$\frac{c}{b}$$ and $$\frac{a}{b}$$,

$$\frac{c}{b} + \frac{a}{b} = \frac{m}{n} \ , \ \frac{c}{b} - \frac{a}{b} = \frac{n}{m}$$

$$\frac{c}{b} = \frac{1}{2} \Bigg (\frac{m}{n} + \frac{n}{m} \Bigg) = \frac{m^2+n^2}{2mn}$$

$$\frac{a}{b} = \frac{1}{2} \Bigg (\frac{m}{n} - \frac{n}{m} \Bigg) = \frac{m^2-n^2}{2mn}$$

Hence is the result be obtained above,

$$a = m^2-n^2$$

$$b = 2mn$$

$$c = m^2+n^2$$

## Examples
**There are infinite Pythagorean triplets as there are infinite odd numbers.**
{: .text-justify}

There are 16 primitive Pythagorean triples with c ≤ 100:
{: .text-justify}

$$(3, 4, 5) ,	(5, 12, 13) ,	(8, 15, 17) ,	(7, 24, 25)$$

$$(20, 21, 29) ,	(12, 35, 37) ,	(9, 40, 41) ,	(28, 45, 53)$$

$$(11, 60, 61) ,	(16, 63, 65) ,	(33, 56, 65) ,	(48, 55, 73)$$

$$(13, 84, 85) ,	(36, 77, 85) ,	(39, 80, 89) ,	(65, 72, 97)$$

## Code

### Naive Approach
```ruby
/**
 * A naive pythagorean triplet generator
 *
 * @param limit
 *            : maximum value of c
 *
 * @return a list of all the pythagorean triplets
 */
public static ArrayList<int[]> naivePythagoreanTripletsGenerator(int limit) {
  ArrayList<int[]> triplets = new ArrayList<>();

  for (int a = 3; a <= limit; a++) {
    for (int b = a + 1; b <= limit; b++) {
      for (int c = b + 1; c <= limit; c++) {
        if (a * a + b * b == c * c) {
          triplets.add(new int[] { a, b, c });
        }
      }
    }
  }
  return triplets;
}
```

### Euclid's Formula for Primitive Triplets
```ruby
/**
 * A function to calculate the gcd of 2 given numbers
 *
 * @param a
 *            first number
 * @param b
 *            second number
 * @return gcd of two numbers
 */
public static int gcd(int a, int b) {
  return a == 0 ? b : gcd(b % a, a);
}

/**
 * A function for Euclid's Formula for pythagorean triplet generator
 *
 * @param limit
 *            : maximum value of c
 *
 * @return a list of all the pythagorean triplets
 */
public static ArrayList<int[]> pythagoreanTripletsGenerator(int limit) {
  ArrayList<int[]> triplets = new ArrayList<>();

  for (int m = 1; m < Math.sqrt(limit); m++) {
    for (int n = 1 + (m % 2); n < m; n += 2) {
      int a = m * m - n * n;
      int b = 2 * m * n;
      int c = m * m + n * n;
      if (c > limit) {
        break;
      }
      if (gcd(gcd(a, b), c) == 1) {
        triplets.add(new int[] { a, b, c });

      }
    }
  }

  return triplets;
}
```


## References and Further Readings
* [Wikipedia](https://en.wikipedia.org/wiki/Pythagorean_triple)
* [http://www.friesian.com/pythag.htm](http://www.friesian.com/pythag.htm)
