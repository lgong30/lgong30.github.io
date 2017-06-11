---
layout: post
title: A Logarithmic Solution for XOR of Consecutive Integers
categories: [skill]
tags: [algorithm]
---

In this post, we will deal with the following XOR problem. Given $l$ consecutive nonnegative integers which start from $s$, _i.e.,_ $s, s+1, \cdots, s + l - 1$, you are asked to get the XOR of them, _i.e.,_ $XOR_{x\in [s+l-1]\setminus [s-1]}x$, where $[s]=\{1,2,\cdots,s\}$. An algorithm with complexity $O(l\log (s + l))$ is straightforward: XOR these numbers one by one (see the following pseudo-code). 

```python
def XOR(s, l):
    x = 0
    for s in xrange(s, s + l):
        x ^= s # note, for general case, you have to implement your own XOR for long-bit integers
    return x
```


Logarithmic Solution
--------------------

Now, let's see a logarithmic solution, _i.e.,_ an algorithm with complexity $O(\log (s + l))$. 

As we know, XOR of multiple single-bit variable (_i.e.,_ $0$ or $1$) equals $1$ if the number of $1$'s is odd, otherwise $0$. Now, 
we decompose the XOR of $[s+l-1]\setminus [s-1]$ by bits, for the $i^{th}$ bit, we only need count how many 1's. It appears that we still need $O(l)$ time to do the counting. However, the consecutiveness of these numbers make the appearance of $1$'s and $0$'s periodic. For example, for the $3^{rd}$ bit (from the lowest bit), roughly speaking the pattern is as follows.

$$\cdots,0,0,0,0,1,1,1,1,0,0,0,0,1,1,1,1,\cdots$$

Of course, you need pay a little attention to the beginning and ending parts, since $l$ might not divide $2^3$.

Generally, 
+ for the $k^{th}$ ($k>1$) bit you only need to count how many $1$'s are they in the first and last partial period (if applicable). Since there are always even number of $1$'s in a full period.
+ for the first bit, clearly $1$'s appear $\lfloor\frac{l - b}{2}\rfloor + b$ times


The following pseudo-code shows how to XOR the $i^{th}$ bit. Clearly, it can be done in $O(\log(s + l))$, as there are at most $\log (s + l)$ bits, therefore, this algorithm can calculate the XOR in $O(\log^2(s+l))$ time. Note that, before calculating the XOR bit-by-bit, you should first get these bits and after finishing the XOR, you should assemble these bits into a decimal number. Clearly, these two operations can be done in $O(\log(s+l))$.


```python
# base = 2 ** i
# bit is the value of the i-th bit
# r[i] is the i-th bit for the result
if base == 1:
    r[i] = ((l - bit) / 2 + bit) % 2
else:
    period = 2 * base
    preamble_len = period - bit * base - s % base
    preamble = min(l, preamble_len)
    if bit == 0:
        preamble = max(0, preamble - (base - s % base))
    padding = 0
    if l > preamble_len:
        padding_len = (l - preamble_len) % period
        padding = padding_len - base if padding_len > base else 0
    
    r[i] = (preamble + padding) % 2
```


