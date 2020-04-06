# Problem Set

Given a non-empty array of integers, every element appears `k` times except for one, which appears exactly `p` time(s) where `p % k != 0`. Find that single one.

# Special Case

We want to use bitwise operation to solve this problem. In order to do that, we need to represent all these integers in binary. Let's start with 1-bit number. Suppose we have an array of 1-bit numbers (`0` or `1`), and we want to construct a m-bit counter `cm,...,c1` such that:

1. When counter hits `0`, it doesn't change.
2. When counter hits `1`, it increase by 1.
3. When counter reaches `k`, it returns to 0.
4. `2^m >= k => m >= log k`

For first two conditions, we use `XOR` operation because, for example, when counter `0000` hits `1`, `c1 = c1 ^ 1 = 0 ^ 1 = 1` and when `0001` hits `0`, `c1 = c1 ^ 0 = 1 ^ 0 = 1`. We can consider `^` as an operation that `c1 = c1 ^ i` means `c1` will increase by 1 depend on the value of `i`  Then how should we update `c2`? `c2` increases by 1 when `c1 == 1` and counter hits `1`, that is `c2 = c2 ^ (c1 & i)`. Similarly, `cm = cm ^ (cm-1 & ... & c1 & i)`.

For third condition, we need a mask such that `mask = 1` when counter reaches `k` and `mask = 0` otherwise, then we can simply let `cm = cm & mask, ... , c1 = c1 & mask`. Write `k` in binary form: `km,...,k1`, then we can construct mask as `mask = ~(ym & ... & y1)` where `yi = ci` when `ki = 1` and `yi = ~ci` when `ki = 0`.

Algorithm Summary:
```java
for (int i : nums) {
    cm ^= (cm-1 & ... & c1 & i);
    cm-1 ^= (cm-2 & ... & c1 & i);
    .....
    c1 ^= i;
    
    mask = ~(y1 & y2 & ... & ym) where yj = cj if kj = 1, and yj = ~cj if kj = 0 (j = 1 to m).

    cm &= mask;
    ......
    c1 &= mask;
}
```

# General Case

Now, we generalize to the case of 32-bit numbers instead of 1-bit numbers. One possible way is to use 32 `m-bit` counters for each bit in the integers. However, we want to use m `32-bit` counters because bit operation is applied to one bit and is independent of other bits. So we have m counters, `cm, ... , c1`, with each have 32-bit, `r-th` bit counts the `r-th` bit of the input numbers. That means if the count of `1` at `r-th` bit of all input numbers is `q` and `q' = q % k = q'm...q'1`, then `r-th` bit of `c1` will equal to `q'1`.

Next problem is what to return. After we scan all the elements in the array, the elements appear `k` times won't contribute to the counters because counters will reset to `0` when they hit `k`. What contributes to counters is the single number which appears `p` times (if `p > k`, the first multiples of `k`s won't contribute, so we can set `p' = p % k`). `p' = p'm...p'1`. We can prove that if `p'j = 1`, then `cj` is equal to the single number.

# Examples

1. `k=2, p=1`

Since `k=2`, `m=1`. Since `2^m = k`, we don't need a mask.

```java
public int singleNumber(int[] nums) {
        int x1 = 0;
         
        for (int i : nums) {
            x1 ^= i;
        }
         
        return x1;
    }
```

2. `k=3, p=1`

Since `k=3`, `m=2`. Since `2^m > k`, we need a mask. `k_2 = '11'` so `mask = ~(x1 & x2)`.

```java
public int singleNumber(int[] nums) {
        int x1 = 0, x2 = 0, mask = 0;
         
        for (int i : nums) {
            x2 ^= x1 & i;
            x1 ^= i;
            mask = ~(x1 & x2);
            x2 &= mask;
            x1 &= mask;
        }

        return x1;  // Since p = 1, in binary form p = '01', then p1 = 1, so we should return x1. 
                    // If p = 2, in binary form p = '10', then p2 = 1, and we should return x2.
                    // Or alternatively we can simply return (x1 | x2).
    }
```
