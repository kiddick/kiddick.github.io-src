Title: Convert numbers between positional numeral systems
Date: 2015-12-30
Category: programming
Tags: python, math

Let's view basic approach to convert numbers between different positional numeral systems on particular example:

We need to convert $336_8$ to decimal.

$336_8 = 3 * 8 ^ 2 + 3 * 8 ^ 1 + 6 * 8 ^ 0 = 3 * 64 + 24 + 6 = 222_{10}$

$l$ - length of initial number, $n$ - base of numeral system, $r$ - result:

$r = x_1 * n^{l -1} + x_2 * n^{l-2} + x_3 * n^{l-3} + ... + x_l*n^0 $

So it is easy to programming with using power function. But there is an another approach. We could use loop for that purpose:

```python
def oct(n):
    r = 0
    for d in n:
        r = r * 8 + int(d)
    return r
```

Some details for example above:

1st iteration $r = n*0 + x_1$

2nd iteration $r = nx_1 + x_2$

3rd iteration $r = n(n*x_1 + x_2) + x_3 = n^2x_1 + nx_2 + x_3$

...

$l$ iteration $r = x_1 * n^{l -1} + x_2 * n^{l-2} + x_3 * n^{l-3} + ... + x_l*n^0 $

Exactly the same result as above.