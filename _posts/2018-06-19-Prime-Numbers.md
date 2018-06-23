---
title: "Prime Numbers"
excerpt_separator: "<!--more-->"
categories:
  - Math
tags:
  - Prime Numbers
toc: true
toc_sticky: true
---

## Definition
A Prime number is a natural number greater than $$1$$ which has no factors execpt itself. Alternatively if a number cannot be formed by multiplying two smaller natural numbers. There are infinite prime numbers. Example of some of prime numbers, $$2, \ 3, \ 5, \ 7, \ 11, \ 13 \dots$$.
{: .text-justify}

## Computing Primes
There are many algorithms to compute prime numbers.
{: .text-justify}

One could start from the simple fact that a prime number has 2 factors one itself and $$1$$. Since we all knows that $$1$$ will divide all natural numbers so its not counted as a factor.
{: .text-justify}

### Basic Approach 1 and Code
Say you want to find out all the primes below a given number $$N$$. From the above knowledge we will run two loops. Outer loop will run from 2 to $$N$$ picking one number at a time and in the inner loop we will simply check if there is any number which is less than picked number and divides it. If there is such a number which divides the picked number we will say its not a prime number.
{: .text-justify}

```ruby
/**
 * A function to calculate prime numbers
 *
 * @param n
 *            max number upto which we have to find primes.
 * @return An array list of all the primes below n.
 */
public static ArrayList<Long> naivePrimeGenerator1(long n) {
  ArrayList<Long> primeList = new ArrayList<>();
  for (long i = 2; i <= n; i++) {
    long numberOfTimesDivides = 0;
    for (long j = 2; j <= i; j++) {
      if (i % j == 0) {
        numberOfTimesDivides++;
      }
      if (numberOfTimesDivides > 1) {
        break;
      }
    }
    if (numberOfTimesDivides == 1) {
      primeList.add(i);
    }
  }
  return primeList;
}
```

### Basic Approach 2 and Code
One can observe that if we are given a number $$N$$, then we dont have to run our inner loop upto $$N$$. Lets say we picked $$M$$ then we can run inner loop till $$M/2$$. Why so ? Think!!!
{: .text-justify}

```ruby
/**
 * A function to calculate prime numbers better than naivePrimeGenerator1
 *
 * @param n
 *            max number upto which we have to find primes.
 * @return An array list of all the primes below n.
 */
public static ArrayList<Long> naivePrimeGenerator2(long n) {
  ArrayList<Long> primeList = new ArrayList<>();
  for (long i = 2; i <= n; i++) {
    long numberOfTimesDivides = 1;
    for (long j = 2; j <= i / 2 && numberOfTimesDivides == 1; j++) {
      if (i % j == 0) {
        numberOfTimesDivides=0;
      }
    }
    if (numberOfTimesDivides == 1) {
      primeList.add(i);
    }
  }
  return primeList;
}
```

### Basic Approach 3 and Code
Another observation which can be made is that running the inner loop upto $$\sqrt{M}$$. This is because whenever $$M = a \cdot b$$ , one of the two factors $$a$$ and $$b$$ is less than or equal to the square root of $$M$$.
{: .text-justify}

```ruby
/**
 * A function to calculate prime numbers better than naivePrimeGenerator2
 *
 * @param n
 *            max number upto which we have to find primes.
 * @return An array list of all the primes below n.
 */
public static ArrayList<Long> naivePrimeGenerator3(long n) {
  ArrayList<Long> primeList = new ArrayList<>();
  for (long i = 2; i <= n; i++) {
    long numberOfTimesDivides = 1;
    for (long j = 2; j*j <= i && numberOfTimesDivides == 1; j++) {
      if (i % j == 0) {
        numberOfTimesDivides=0;
      }
    }
    if (numberOfTimesDivides == 1) {
      primeList.add(i);
    }
  }
  return primeList;
}
```

### Basic Approach 3.1 and Code
Another optimization to Approach $$3$$ is to check only primes as factors in this range. For instance, to check whether $$53$$ is prime, this approach divides it by the primes in the range from $$2$$ to $$\sqrt{53}$$, which are $$2, \ 3, \ 5 \ \text{and} \ 7$$. Each division produces a nonzero remainder, so $$53$$ is indeed prime.
{: .text-justify}

```ruby
/**
 * A function to calculate prime numbers better than naivePrimeGenerator3
 *
 * @param n
 *            max number upto which we have to find primes.
 * @return An array list of all the primes below n.
 */
public static ArrayList<Long> naivePrimeGenerator3_1(long n) {
  ArrayList<Long> primeList = new ArrayList<>();
  primeList.add(2L);
  for (long i = 3; i <= n; i++) {
    long numberOfTimesDivides = 1;
    for (int j = 0; primeList.get(j) * primeList.get(j) <= i && numberOfTimesDivides == 1; j++) {
      if (i % primeList.get(j) == 0) {
        numberOfTimesDivides = 0;
      }
    }
    if (numberOfTimesDivides == 1) {
      primeList.add(i);
    }
  }
  return primeList;
}
```

## Sieve of Eratosthenes

### Basic Algorithm
The algorithm is as follows :
{: .text-justify}

1. Make a list of consecutive numbers from 2 to given number $$N$$, ($$2, \ 3, \ 4, \dots N$$).
2. Since $$p = 2$$ is our first prime number, mark all multiples of $$p$$ i.e : $$2p, \ 3p, \ 4p\dots$$ i.e $$2 \ - 4, \ 6, \ 8 \dots$$.
3. The next prime number will be the first number which is not marked.
4. Mark all the multiples of the prime number which was obtained in previous step upto $$N$$.
5. Repeat steps 3 and 4 until you reach a number that is greater than $$\sqrt{N}$$.
6. All the remaining unmarked numbers in the list are prime.
{: .text-justify}

The main idea here is that every value given to p will be prime, because if it were composite it would be marked as a multiple of some other, smaller prime.
{: .notice--info}

Following image will show you the above process in action.
{: .text-justify}

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/Sieve_of_Eratosthenes_animation.gif){: .align-center}
[Sieve of Eratosthenes: algorithm steps for primes below 121 (including optimization of starting from prime's square).](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes#/media/File:Sieve_of_Eratosthenes_animation.gif){: style="text-align: center;"}

### Optimization
Its easy to notice that since every alternative number is an even number there is no need to check them and just simply check all the odd numbers above $$2$$. This will reduce our further calculations.
{: .text-justify}

As a refinement, it is sufficient to mark the numbers in step 2 starting from $$p^2$$, as all the smaller multiples of $$p$$ will have already been marked at that point. This means that the algorithm is allowed to terminate in step 4 when $$p^2$$ is greater than $$n$$.
{: .text-justify}

### Code
```ruby
/**
 * A function to illustrate Sieve of Eratosthenes for prime generation
 *
 * @param n
 *            max number upto which we have to find primes.
 * @return An array list of all the primes below n.
 */
public static ArrayList<Integer> sieveOfEratosthene(int n) {

  ArrayList<Integer> primeList = new ArrayList<>();

  primeList.add(2);

  if (n == 2) {
    return primeList;
  }

  boolean prime[] = new boolean[n + 1];

  for (int p = 3; p * p <= n; p = p + 2) {
    if (prime[p] == false) {
      for (int i = p * p; i <= n; i += p) {
        prime[i] = true;
      }
    }
  }

  for (int i = 3; i < n; i = i + 2) {
    if (!prime[i]) {
      primeList.add(i);
    }
  }
  for (int i : primeList) {
    System.out.print(i + " ");
  }
  return primeList;
}
```

### Complexity
Time Complexity = $$O(n \log (\log n))$$ operations [Why?](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes#Computational_analysis) \\
Space Complexity = $$O(n)$$ memory.

## Segmented Sieve of Eratosthenes:

### Limitations of Sieve of Eratosthenes
Any computer programs efficiency depends upon time and memory. In computer world these two things are always inversely proportional to each other. Sieve of Eratosthenes suffers from memory it requires to compute primes. And since its also not cache friendly, its hard to do find primes for bigger inputs.
{: .text-justify}

### Segmented Sieve:
The concept is to divide the input, $$n$$, into different segments and compute primes in each segment. This algorithm basically sieves some of the initial primes based on the input, $$n$$. Lets see the steps in this algorithm,
{: .text-justify}

1. Divide each segment such that the size of each segment is at-most $$\sqrt{n}$$.
2. Using Sieve of Eratosthenes find all the primes in the first segment below $$\sqrt{n}$$ and store them in an array.
3. For every segment other than first segment, we will make two variable $$segmentStart$$ and $$segmentEnd$$ to keep track of current segment start and end points respectively.
  - $$segmentStart$$ and $$segmentEnd$$ will be initialized after completion of one segment by $$segmentLength$$.
  - Create a temporary array just like we did in Sieve of Eratosthenes to mark the primes.
  - Loop over all primes found in step 1 and mark its multiples in the current segment.
{: .text-justify}

### Code
```ruby
/**
 * A function to illustrate segmented Sieve of Eratosthenes
 *
 * @param n
 *            max number upto which we have to find primes.
 * @return An array list of all the primes below n.
 */
public static ArrayList<Integer> segmentedSeive(int n) {

  int segmentLength = (int) (Math.floor(Math.sqrt(n)) + 1);
  ArrayList<Integer> initialPrimeList = sieveOfEratosthenes(segmentLength);

  ArrayList<Integer> primeList = new ArrayList<>();
  primeList.addAll(initialPrimeList);

  int segmentStart = segmentLength;
  int segmentEnd = 2 * segmentLength;

  while (segmentStart < n) {

    if (segmentEnd >= n) {
      segmentEnd = n;
    }

    boolean prime[] = new boolean[segmentLength + 1];

    for (int i = 0; i < initialPrimeList.size(); i++) {

      int lowerLimit = (int) (Math.floor(segmentStart / initialPrimeList.get(i)) * initialPrimeList.get(i));

      if (lowerLimit < segmentStart) {
        lowerLimit += initialPrimeList.get(i);
      }

      for (int j = lowerLimit; j <= segmentEnd; j += initialPrimeList.get(i)) {
        prime[j - segmentStart] = true;
      }
    }

    for (int i = segmentStart; i <= segmentEnd; i++) {
      if (!prime[i - segmentStart]) {
        primeList.add(i);
      }
    }

    segmentStart = segmentStart + segmentLength;
    segmentEnd = segmentEnd + segmentLength;
  }

  return primeList;
}
```

### Complexity
Time Complexity = $$O(n \log (\log n))$$ operations \\
Space Complexity = $$O(\sqrt{n})$$ memory.

## Sieve of Atkins
The algorithm is governed by a few set of rules, which are as follows:
{: .text-justify}

1. Create a results list, filled with $$2, \ 3, \ and \ 5$$.
2. Create a sieve list with an entry for each positive integer; all entries of this list should initially be marked non prime.
3. For each entry number n in the sieve list, with modulo-sixty remainder r:
  - If $$r$$ is $$1, \ 13, \ 17, \ 29, \ 37, \ 41, \ 49, \ or \ 53$$, flip the entry for each possible solution to $$4x^2 + y^2 = n$$.
  - If $$r$$ is $$7, \ 19, \ 31, \ or \ 43$$, flip the entry for each possible solution to $$3x^2 + y^2 = n$$.
  - If $$r$$ is $$11, \ 23, \ 47, \ or \ 59$$, flip the entry for each possible solution to $$3x^2 – y^2 = n$$ when $$x > y$$.
  - If $$r$$ is something else, ignore it completely..
4. Start with the lowest number in the sieve list.
5. Take the next number in the sieve list still marked prime.
6. Include the number in the results list.
7. Square the number and mark all multiples of that square as non prime. Note that the multiples that can be factored by $$2, \ 3, \ or \ 5$$ need not be marked, as these will be ignored in the final enumeration of primes.
8. Repeat steps four through seven.
{: .text-justify}

Compared with the Sieve of Eratosthenes, where we marks off multiples of primes, Sieve of Atkins does some preliminary work and then marks off multiples of squares of primes, hence has a better theoretical asymptotic complexity.
{: .text-justify}

### Code
```ruby
/**
 * A function to illustrate Sieve of Atkin for prime generation
 *
 * @param n
 *            max number upto which we have to find primes.
 * @return An array list of all the primes below n.
 */
static ArrayList<Integer> sieveOfAtkin(int n) {
  ArrayList<Integer> primeList = new ArrayList<>();

  if (n > 2) {
    primeList.add(2);
  }
  if (n > 3) {
    primeList.add(3);
  }

  boolean numberArray[] = new boolean[n];

  for (int i = 0; i < n; i++)
    numberArray[i] = false;

  for (int x = 1; x * x < n; x++) {
    for (int y = 1; y * y < n; y++) {

      int m = (4 * x * x) + (y * y);
      if (m <= n && (m % 12 == 1 || m % 12 == 5)) {

        numberArray[m] ^= true;
      }

      m = (3 * x * x) + (y * y);
      if (m <= n && m % 12 == 7) {
        numberArray[m] ^= true;
      }
      m = (3 * x * x) - (y * y);
      if (x > y && m <= n && m % 12 == 11) {
        numberArray[m] ^= true;
      }
    }
  }

  for (int r = 5; r * r < n; r++) {
    if (numberArray[r]) {
      for (int i = r * r; i < n; i += r * r) {
        numberArray[i] = false;
      }
    }
  }

  for (int i = 5; i < n; i++) {
    if (numberArray[i]) {
      primeList.add(i);
    }
  }
  return primeList;
}
```


### Complexity
Time Complexity = $$O(N /{log (log N)})$$ [Why ?](https://en.wikipedia.org/wiki/Sieve_of_Atkin#Computational_complexity)

## References and Further Readings
* [Prime Numbers](https://en.wikipedia.org/wiki/Prime_number)
* [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)
* [Sieve of Atkin](https://en.wikipedia.org/wiki/Sieve_of_Atkin)
