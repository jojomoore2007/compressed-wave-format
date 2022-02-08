Using a set of waves and operations, one can generate a reasonably accurate waveform that can be stored in significantly less space.

The idea is to use the following operations to do so (written in RPN):

- x y add
- x y sub
- x y mul
- x y div
- x y pow
- x y min
- x y max
- x floor
- x ceil
- x round
- x y cmp

We can then create the following 16 tokens:

- 0: following 4 bits (acts like NOP when there are none left)
- 1: wave 1
- 2: wave 2
- 3: wave 3
- 4: x
- 5: add
- 6: sub
- 7: mul
- 8: div
- 9: pow
- A: min
- B: max
- C: floor
- D: ceil
- E: round
- F: compare

Building with these, we can form the following example with RPN, which creates a reasonably accurate square wave based on the Fourier transform (w=sin):

x w 3 x mul w 3 div add 5 x mul w 5 div add 7 x mul w 7 div add

We can then convert this to the following sequence of tokens:
```
41034710385054710585074710785
```
13 tokens = 52 bits  
52 bits = 7 bytes (the last byte is padded with 0 as a NOP)

However, this isn't the best way to compress a square wave.

The best way to compress it would be with the compare operation.
