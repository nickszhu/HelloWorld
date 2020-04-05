# Problem Set

Given a non-empty array of integers, every element appears `k` times except for one, which appears exactly `p` time(s) where `p % k != 0`. Find that single one.

# Special Case

We want to use bitwise operation to solve this problem. In order to do that, we need to represent all these integers in binary. Let's start with 1-bit number. Suppose we have an array of 1-bit numbers (0 or 1), and we want to construct a m-bit counter `cm,...,c1` such that:

1. When counter hits `0`, it doesn't change.
2. When counter hits `1`, it increase by 1.
3. When counter reaches `k`, it returns to 0.
4. `2^m >= k => m >= log k`

For first two conditions, we use `XOR` operation because, for example, when counter `0000` hits `1`, `c1 = c1 ^ 1 = 0 ^ 1 = 1` and when `0001` hits `0`, `c1 = c1 ^ 0 = 1 ^ 0 = 1`. We can consider `^` as an operation that `c1 = c1 ^ i` means `c1` will increase by 1 depend on the value of `i`  Then how should we update `c2`? `c2` increases by 1 when `c1 == 1` and counter hits 1, that is `c2 = c2 ^ (c1 & i)`. Similarly, `cm = cm ^ (cm-1 & ... & c1 & i)`.

For third condition, we need a mask

