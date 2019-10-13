# general / 2Warm

> Points: 50 \
> previous warm | [next warm](../LetsWarmUp)

## Question

> Can you convert the number 42 (base 10) to binary (base 2)?

### Hint

> Submit your answer in our competition's flag format.
> For example, if you answer was '11111', you would submit 'picoCTF{11111}' as the flag.

## Solution

Binary uses the powers of two instead of powers of ten.
For example, 15 is 1×10<sup>1</sup> + 5×10<sup>0</sup>.
The powers of two less than 42 are 1, 2, 4, 8, 16, 32.

42 - 32 = 10, 10 - 8 = 2, 2 - 2 = 0, therefore 42 = 32 + 8 + 2.

Representing with exponents on two, 42 = 2<sup>5</sup> + 2<sup>3</sup> + 2<sup>1</sup>. This corresponds to binary 101010<sub>2</sub>.

### Flag

`picoCTF{101010}`
