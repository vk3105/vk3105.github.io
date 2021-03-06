---
title: "Prime Factorization and Applications"
excerpt_separator: "<!--more-->"
categories:
  - Math
tags:
  - Prime Factorization
  - Prime Numbers
toc: true
toc_sticky: true
---

## Definitions
**Factors** : The parts that make up the whole number. The factors of a number are the numbers that, when multiplied together, make up the original number.
{: .text-justify}

For example, factors of $$8$$ could be $$2$$ and $$4$$ because $$2 * 4$$ is $$8$$.
{: .text-justify}

**Prime Factorization** : The factorization of a number, $$n$$, into its constituent primes, also called prime decomposition. Given a positive integer $$n \geq 2$$, the prime factorization is written as,
{: .text-justify}

$$n=p_1^{a_1} \times p_2^{a_2} \times \dots \times p_k^{a_k}$$

For example $$n = 60$$,
{: .text-justify}

$$Factorization \ = \ 2^2 \times 3 \times 5 \\
Prime \ Factors \ = \ 2 \ , \ 3 \ and \ 5 \\
Factors \ = \ 1  ,  2  ,  3  ,  4  ,  5  ,  6  ,  10  , 12 ,  16  ,  20  ,  30 \ and \ 60 $$


## Concept and Theory

### Naive Approach
The obvious approach which comes to mind is run a loop from $$1$$ to $$n$$ and check which numbers divides $$n$$ completely. Those will be our all factors.
{: .text-justify}
For prime factors we need to find all the prime numbers in all the factors obtained above.  
{: .text-justify}

```ruby
static void printDivisors(long n) {
  for (long i = 1; i <= n; i++) {
    if (n % i == 0) {
      System.out.print(i + " ");
    }
  }
}
```

### Complexity
Since we are iterating from $$1$$ to $$N$$ complexity will be $$O(N)$$, where $$N$$ is the input number.
{: .text-justify}

### A better solution
One can observe that among any two factors whose product is the given number, one is smaller than $$\sqrt{n}$$ and one is bigger than $$\sqrt{n}$$.
{: .text-justify}

```ruby
public static void printDivisors(long n) {
  for (long i = 1; i <= Math.sqrt(n); i++) {
    if (n % i == 0) {
      if (n / i == i) {
        System.out.print(i + " ");
      } else {
        System.out.print(i + " " + (n / i) + " ");
      }
    }
  }
}
```
Note : we are omitting one factor if its a square. For example $$25$$, we will count $$5$$ once.
{: .notice--info}

### Complexity
Since we are iterating from $$1$$ to $$\sqrt{N}$$ complexity will be $$O(\sqrt{N})$$, where $$N$$ is the input number.
{: .text-justify}

## Concept and Theory for Prime Factorization
Prime factors can be calculated by some precalulations or calculating at runtime. It will depend upon how often you have to factorize a number. If you have to do multiple queries than precalculations is optimal else if once or twice than runtime will be better.
{: .text-justify}

By precalulations I meant storing the prime numbers below the maximum number you would expect in a given situation by using [Sieve of eratosthenes](/math/Prime-Numbers/#sieve-of-eratosthenes).
{: .text-justify}

You can get the prime list from this site too [Prime List](http://www.primos.mat.br/indexen.html).
{: .text-justify}

### Code
```ruby
/*
 * List of first 1000 primes. Max range of number which we can check is INT_MAX
 */
private static final long primes[] = { 2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71,
    73, 79, 83, 89, 97, 101, 103, 107, 109, 113, 127, 131, 137, 139, 149, 151, 157, 163, 167, 173, 179, 181,
    191, 193, 197, 199, 211, 223, 227, 229, 233, 239, 241, 251, 257, 263, 269, 271, 277, 281, 283, 293, 307,
    311, 313, 317, 331, 337, 347, 349, 353, 359, 367, 373, 379, 383, 389, 397, 401, 409, 419, 421, 431, 433,
    439, 443, 449, 457, 461, 463, 467, 479, 487, 491, 499, 503, 509, 521, 523, 541, 547, 557, 563, 569, 571,
    577, 587, 593, 599, 601, 607, 613, 617, 619, 631, 641, 643, 647, 653, 659, 661, 673, 677, 683, 691, 701,
    709, 719, 727, 733, 739, 743, 751, 757, 761, 769, 773, 787, 797, 809, 811, 821, 823, 827, 829, 839, 853,
    857, 859, 863, 877, 881, 883, 887, 907, 911, 919, 929, 937, 941, 947, 953, 967, 971, 977, 983, 991, 997,
    1009, 1013, 1019, 1021, 1031, 1033, 1039, 1049, 1051, 1061, 1063, 1069, 1087, 1091, 1093, 1097, 1103, 1109,
    1117, 1123, 1129, 1151, 1153, 1163, 1171, 1181, 1187, 1193, 1201, 1213, 1217, 1223, 1229, 1231, 1237, 1249,
    1259, 1277, 1279, 1283, 1289, 1291, 1297, 1301, 1303, 1307, 1319, 1321, 1327, 1361, 1367, 1373, 1381, 1399,
    1409, 1423, 1427, 1429, 1433, 1439, 1447, 1451, 1453, 1459, 1471, 1481, 1483, 1487, 1489, 1493, 1499, 1511,
    1523, 1531, 1543, 1549, 1553, 1559, 1567, 1571, 1579, 1583, 1597, 1601, 1607, 1609, 1613, 1619, 1621, 1627,
    1637, 1657, 1663, 1667, 1669, 1693, 1697, 1699, 1709, 1721, 1723, 1733, 1741, 1747, 1753, 1759, 1777, 1783,
    1787, 1789, 1801, 1811, 1823, 1831, 1847, 1861, 1867, 1871, 1873, 1877, 1879, 1889, 1901, 1907, 1913, 1931,
    1933, 1949, 1951, 1973, 1979, 1987, 1993, 1997, 1999, 2003, 2011, 2017, 2027, 2029, 2039, 2053, 2063, 2069,
    2081, 2083, 2087, 2089, 2099, 2111, 2113, 2129, 2131, 2137, 2141, 2143, 2153, 2161, 2179, 2203, 2207, 2213,
    2221, 2237, 2239, 2243, 2251, 2267, 2269, 2273, 2281, 2287, 2293, 2297, 2309, 2311, 2333, 2339, 2341, 2347,
    2351, 2357, 2371, 2377, 2381, 2383, 2389, 2393, 2399, 2411, 2417, 2423, 2437, 2441, 2447, 2459, 2467, 2473,
    2477, 2503, 2521, 2531, 2539, 2543, 2549, 2551, 2557, 2579, 2591, 2593, 2609, 2617, 2621, 2633, 2647, 2657,
    2659, 2663, 2671, 2677, 2683, 2687, 2689, 2693, 2699, 2707, 2711, 2713, 2719, 2729, 2731, 2741, 2749, 2753,
    2767, 2777, 2789, 2791, 2797, 2801, 2803, 2819, 2833, 2837, 2843, 2851, 2857, 2861, 2879, 2887, 2897, 2903,
    2909, 2917, 2927, 2939, 2953, 2957, 2963, 2969, 2971, 2999, 3001, 3011, 3019, 3023, 3037, 3041, 3049, 3061,
    3067, 3079, 3083, 3089, 3109, 3119, 3121, 3137, 3163, 3167, 3169, 3181, 3187, 3191, 3203, 3209, 3217, 3221,
    3229, 3251, 3253, 3257, 3259, 3271, 3299, 3301, 3307, 3313, 3319, 3323, 3329, 3331, 3343, 3347, 3359, 3361,
    3371, 3373, 3389, 3391, 3407, 3413, 3433, 3449, 3457, 3461, 3463, 3467, 3469, 3491, 3499, 3511, 3517, 3527,
    3529, 3533, 3539, 3541, 3547, 3557, 3559, 3571, 3581, 3583, 3593, 3607, 3613, 3617, 3623, 3631, 3637, 3643,
    3659, 3671, 3673, 3677, 3691, 3697, 3701, 3709, 3719, 3727, 3733, 3739, 3761, 3767, 3769, 3779, 3793, 3797,
    3803, 3821, 3823, 3833, 3847, 3851, 3853, 3863, 3877, 3881, 3889, 3907, 3911, 3917, 3919, 3923, 3929, 3931,
    3943, 3947, 3967, 3989, 4001, 4003, 4007, 4013, 4019, 4021, 4027, 4049, 4051, 4057, 4073, 4079, 4091, 4093,
    4099, 4111, 4127, 4129, 4133, 4139, 4153, 4157, 4159, 4177, 4201, 4211, 4217, 4219, 4229, 4231, 4241, 4243,
    4253, 4259, 4261, 4271, 4273, 4283, 4289, 4297, 4327, 4337, 4339, 4349, 4357, 4363, 4373, 4391, 4397, 4409,
    4421, 4423, 4441, 4447, 4451, 4457, 4463, 4481, 4483, 4493, 4507, 4513, 4517, 4519, 4523, 4547, 4549, 4561,
    4567, 4583, 4591, 4597, 4603, 4621, 4637, 4639, 4643, 4649, 4651, 4657, 4663, 4673, 4679, 4691, 4703, 4721,
    4723, 4729, 4733, 4751, 4759, 4783, 4787, 4789, 4793, 4799, 4801, 4813, 4817, 4831, 4861, 4871, 4877, 4889,
    4903, 4909, 4919, 4931, 4933, 4937, 4943, 4951, 4957, 4967, 4969, 4973, 4987, 4993, 4999, 5003, 5009, 5011,
    5021, 5023, 5039, 5051, 5059, 5077, 5081, 5087, 5099, 5101, 5107, 5113, 5119, 5147, 5153, 5167, 5171, 5179,
    5189, 5197, 5209, 5227, 5231, 5233, 5237, 5261, 5273, 5279, 5281, 5297, 5303, 5309, 5323, 5333, 5347, 5351,
    5381, 5387, 5393, 5399, 5407, 5413, 5417, 5419, 5431, 5437, 5441, 5443, 5449, 5471, 5477, 5479, 5483, 5501,
    5503, 5507, 5519, 5521, 5527, 5531, 5557, 5563, 5569, 5573, 5581, 5591, 5623, 5639, 5641, 5647, 5651, 5653,
    5657, 5659, 5669, 5683, 5689, 5693, 5701, 5711, 5717, 5737, 5741, 5743, 5749, 5779, 5783, 5791, 5801, 5807,
    5813, 5821, 5827, 5839, 5843, 5849, 5851, 5857, 5861, 5867, 5869, 5879, 5881, 5897, 5903, 5923, 5927, 5939,
    5953, 5981, 5987, 6007, 6011, 6029, 6037, 6043, 6047, 6053, 6067, 6073, 6079, 6089, 6091, 6101, 6113, 6121,
    6131, 6133, 6143, 6151, 6163, 6173, 6197, 6199, 6203, 6211, 6217, 6221, 6229, 6247, 6257, 6263, 6269, 6271,
    6277, 6287, 6299, 6301, 6311, 6317, 6323, 6329, 6337, 6343, 6353, 6359, 6361, 6367, 6373, 6379, 6389, 6397,
    6421, 6427, 6449, 6451, 6469, 6473, 6481, 6491, 6521, 6529, 6547, 6551, 6553, 6563, 6569, 6571, 6577, 6581,
    6599, 6607, 6619, 6637, 6653, 6659, 6661, 6673, 6679, 6689, 6691, 6701, 6703, 6709, 6719, 6733, 6737, 6761,
    6763, 6779, 6781, 6791, 6793, 6803, 6823, 6827, 6829, 6833, 6841, 6857, 6863, 6869, 6871, 6883, 6899, 6907,
    6911, 6917, 6947, 6949, 6959, 6961, 6967, 6971, 6977, 6983, 6991, 6997, 7001, 7013, 7019, 7027, 7039, 7043,
    7057, 7069, 7079, 7103, 7109, 7121, 7127, 7129, 7151, 7159, 7177, 7187, 7193, 7207, 7211, 7213, 7219, 7229,
    7237, 7243, 7247, 7253, 7283, 7297, 7307, 7309, 7321, 7331, 7333, 7349, 7351, 7369, 7393, 7411, 7417, 7433,
    7451, 7457, 7459, 7477, 7481, 7487, 7489, 7499, 7507, 7517, 7523, 7529, 7537, 7541, 7547, 7549, 7559, 7561,
    7573, 7577, 7583, 7589, 7591, 7603, 7607, 7621, 7639, 7643, 7649, 7669, 7673, 7681, 7687, 7691, 7699, 7703,
    7717, 7723, 7727, 7741, 7753, 7757, 7759, 7789, 7793, 7817, 7823, 7829, 7841, 7853, 7867, 7873, 7877, 7879,
    7883, 7901, 7907, 7919 };

/**
 * A function to check out of bounds for a given number
 *
 * @param num Given number to test
 * @return True if value is greater than Integer.MAX_VALUE else false
 */
private static boolean isOutOfRangeMax(long num) {
  return num > Integer.MAX_VALUE ? true : false;
}

/**
 * A function to check out of bounds for a given number
 *
 * @param num Given number to test
 * @return True if value is less than 0 else false
 */
private static boolean isOutOfRangeMin(long num) {
  return num < 0 ? true : false;
}

/**
 * A function to generate all the divisors pairs(prime divisor, power)
 *
 * @param num Given number to test
 * @return List of all the prime factor of given number
 * @throws Exception
 */
public static ArrayList<long[]> getPrimeFactors(long num) throws Exception {

  if (isOutOfRangeMax(num)) {
    throw new Exception("Value given is larger than Integer.MAX_VALUE.");
  }

  if (isOutOfRangeMin(num)) {
    throw new Exception("Value given is less than 0.");
  }

  ArrayList<long[]> factorList = new ArrayList<>();

  long sqrt = (long) Math.sqrt(num);
  int i = 0;
  for (; i < primes.length && num != 1 && primes[i] <= sqrt; i++) {
    long count = 0;
    while (num % primes[i] == 0) {
      count++;
      num /= primes[i];
    }
    if (count != 0) {
      factorList.add(new long[] { primes[i], count });
    }
  }

  if (num != 1) {
    factorList.add(new long[] { num, 1 });
  }

  return factorList;
}
```

### Complexity
Since we are iterating from $$1$$ to $$\sqrt{N}$$ complexity will be $$O(\sqrt{N})$$, where $$N$$ is the input number.
{: .text-justify}

## Finding Factors using Prime Factorization
Using above functions one can write another way for finding factors as follows,
{: .text-justify}

### Code
```ruby
/**
 * A function to generate all the divisors list
 *
 * @param num Given number to test
 * @return List of all the divisors of given number
 * @throws Exception
 */
public static ArrayList<Long> getDivisorsList(long num) throws Exception {
  ArrayList<long[]> factorList = getPrimeFactors(num);
  ArrayList<Long> divisorList = new ArrayList<>();
  if (factorList == null) {
    return null;
  }
  divisorList.add(1L);

  for (long[] arr : factorList) {
    int size = divisorList.size();
    for (int j = 0; j < size; j++) {
      for (long i = 1; i <= arr[1]; i++) {
        divisorList.add((long) (Math.pow(arr[0], i) * divisorList.get(j)));
      }
    }
  }

  return divisorList;
}
```

## Number of Factors of a Given Number  
One can find out the number of factors for a given number $$N$$ using prime factorization.
{: .text-justify}

Suppose $$N$$ is a power of a prime, $$N = p^{\alpha}$$, then it has $$\alpha + 1$$ factors.
{: .text-justify}

Since each power from $$1$$ to $$\alpha$$ will be a factor. We are adding $$1$$ because $$1$$ will also be a factor.
{: .text-justify}

Now lets say,
{: .text-justify}

$$N = p^{\alpha} \times q^{\beta} \dots r^{\gamma}$$

We can argue from the above example that for prime $$p$$ we have $$\alpha + 1$$ factors, for $$q$$ we have $$\beta + 1$$ factors and so on. Thus we can say if we multiply all of them we will get our count i.e.
{: .text-justify}

$$Factors \ of \ N \ = (\alpha + 1)(\beta + 1) \dots (\gamma + 1) $$

If above things are not clear we see it in more depth via an example,
{: .text-justify}

Lets say we have $$36$$ whose prime factorization is given as below,
{: .text-justify}

$$36 = 2^2 \times 3^2$$

Prime number $$2$$ alone will give us $$1$$, $$2$$ and $$4$$ as prime factors and prime number $$3$$ alone will give us $$1$$, $$3$$ and $$9$$.
{: .text-justify}

So what factor will we will get when prime factors of $$2$$ and $$3$$ are used together ? We can take no $$2$$ at all or no $$3$$ at all or we can take one $$2$$ and no $$3$$ or we can take two $$2$$ and one $$3$$ etc. All we know is we need to find all the possible combinations of these factors.  
{: .text-justify}

$$ No \ 2 \ and \ no \ 3 = 1 \\
No \ 2 \ and \ one \ 3 = 3 \\
No \ 2 \ and \ two \ 3 = 9 \\
One \ 2 \ and \ no \ 3 = 2 \\
One \ 2 \ and \ one \ 3 = 6 \\
One \ 2 \ and \ two \ 3 = 18 \\
Two \ 2 \ and \ no \ 3 = 4 \\
Two \ 2 \ and \ one \ 3 = 12 \\
Two \ 2 \ and \ two \ 3 = 36 $$

$$All \ Factors = 1 , 2, 3, 4, 6, 9, 12, 18 \ and \ 36 \\
Total \ Count \ of \ Factors = 9 $$

Or,

$$36 = 2^2 \times 3^2 \\
Total \ Count \ of \ Factors = (2+1)(2+1) = 9$$

### Code
```ruby
/**
 * A function to count the divisors
 *
 * @param num Given number to test
 * @return Count of divisors of given number
 * @throws Exception
 */
public static int getDivisorsCount(long num) throws Exception {
  int res = 1;
  ArrayList<long[]> factorList = getPrimeFactors(num);

  if (factorList == null) {
    return 0;
  }

  for (long[] arr : factorList) {
    res *= (1 + arr[1]);
  }

  return res;
}
```

## Sum of Factors of a Given Number
Another application of prime factorization is finding the sum of all the factors. Lets see the following example again,
{: .text-justify}

$$N = p^{\alpha} \times q^{\beta} \dots r^{\gamma}$$

We knows that the prime $$p$$ will give us following factors
{: .text-justify}

$$p's \ Factors \ = \ 1, p^1 , p^2 , \dots , p^{\alpha} \times \\
q's \ Factors \ = \ 1, q^1 , q^2 , \dots , q^{\alpha} \times \\
\dots \times \\
r's \ Factors \ = \ 1, r^1 , r^2 , \dots , r^{\alpha}$$

So as we did in counting the factors we can do the same and since we needed the sum so above expression can be written as follows,
{: .text-justify}

$$N = (1+ p^1 + p^2 + \dots + p^{\alpha}) \\
(1+q^1 + q^2 + \dots + q^{\alpha}) \\
\dots \\
(1+r^1 + r^2 + \dots + r^{\alpha})$$

This, $$(p^1 + p^2 + \dots + p^{\alpha})$$, can be seen as a sum of GP(Geometric progression).  
{: .text-justify}

The sum of first $$n$$ terms of GP with first term $$a$$, common difference as $$r$$ is given as,
{: .text-justify}

$$Sum \ of \ GP \ = \ \frac{a(r^n-1)}{r-1}$$

Again we can use the function for factorization and find the sum.
{: .text-justify}

### Code
```ruby
/**
 * A function to calculate the sum of a GP
 *
 * @param num the first term
 * @param pow number of terms
 * @return the sum of GP
 */
private static long sumOfGP(long num, long pow) {
  return (long) (Math.pow(num, pow + 1) - 1) / (num - 1);
}

/**
 * A function that returns the sum of all the factors of a number
 *
 * @param num : given number
 *
 * @return : the sum of all factors
 *
 * @throws Exception
 */
public static long getDivisorsSum(long num) throws Exception {
  long res = 1;
  ArrayList<long[]> factorList = getPrimeFactors(num);

  if (factorList == null) {
    return 0;
  }

  for (long[] arr : factorList) {
    res *= (sumOfGP(arr[0], arr[1]));
  }

  return res;
}
```

## References and Further Readings
* [Integer factorization](https://en.wikipedia.org/wiki/Integer_factorization)
* [Prime List](http://www.primos.mat.br/indexen.html)
