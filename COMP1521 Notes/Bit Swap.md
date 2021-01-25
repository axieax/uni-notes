# Bit swap (Week 3 Quiz)

Original solution:

```c
// return value with pairs of bits swapped
uint64_t bit_swap(uint64_t value) {
    uint64_t ans = 0;
    // 32 pairs of bits (starting from left end of bitstring)
    for (int pair = 0; pair < 32; pair++) {
        // Retrieve bit_pair
        uint64_t bit_pair = value >> (31 - pair) * 2;
        // Left shift and write the last bit of bit_pair
        ans = (ans << 1) + (bit_pair & 1);
        // Left shift and write the second last bit of bit_pair
        ans = (ans << 1) + ((bit_pair >> 1) & 1);
    }
    return ans;
}
```

Simplified solution:

```c
// return value with pairs of bits swapped
uint64_t bit_swap(uint64_t value) {
    // Extract odd bits (1010 1010 ... 1010 where each group of 4 is 0xA)
    uint64_t odd_bits = value & 0xAAAAAAAAAAAAAAAA;
    // Extract even bits (0101 0101 ... 0101 where each group of 4 is 0x5)
    uint64_t even_bits = value & 0x5555555555555555;
    // Move odd bits by one to the right and even bits by one to the left
    return (odd_bits >> 1) | (even_bits << 1);
}
```

# Sign flip (flip leftmost bit)

My solution:

```c
// given the 32 bits of a float return it with its sign flipped
uint32_t sign_flip(uint32_t f) {
    // Negate sign and shift to end, then OR remaining bits after it
    return ((~(f >> 31)) << 31) | (f & ((1u << 31) - 1));
}
```

Sample solution:

```c
// given the 32 bits of a float return it with its sign flipped
uint32_t sign_flip(uint32_t f) {
    // XOR flips masked leftmost bit (sign mask)
  	// 0 ^ 1 = 1
  	// 1 ^ 1 = 0
  	return f ^= (1u << 31);
}
```

