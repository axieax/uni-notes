# Code that pulls apart a certain bit range in C

```c
int main(int argc, char *argv[]) {
  assert(argc == 4);
  uint32_t x = strtol(argv[1], NULL, 0);
  int n_bits = 8 * sizeof x;
  int low_bit = strtol(argv[2], NULL, 0);
  int high_bit = strtol(argv[3], NULL, 0);
  
  // Mask
  int mask_size = high_bit - low_bit + 1;
	// ((uint8_t) 1) : 1111 1111
  // say we want 3-5, so 0011 1000
  // Left shifting by mask_size then subtracting one --> mask_size # of 1's at end of string
  uint32_t mask = (((uint64_t) 1) << mask_size) - 1;
  // Left shifting this by low_bits to get in place
  mask = mask << low_bit // or mask <<= low_bit
	
  // Bitwise AND (&) to get rid of the ones we don't want
	uint32_t z = mask & x;
  // Right shift back to end of bit-string to get a number
  z = z >> low_bit // or mask >>= low_bit
	
  printf("%x\n", z);
  return 0;
}
```

- Create a mask (1 everywhere in the range we want to extract)
- Bitwise AND (&) to get rid of the ones we don't want

Application: device drivers

e.g. ./program 0x<u>de</u>adbeef 24 31 --> z = <u>de</u>; ./program 0xde<u>ad</u>beef 16 23 --> z = <u>ad</u>

0xdeadbeef = 0b 1101 1110 1010 1101 1011 1110 1110 1111

lo and hi are 0-indexed, counted from the right-end of bit string

# decimal to hexadecimal

```c
char *int_to_hex_string(uint32_t n) {
  // sizeof returns number of bytes in n's representation (2 hexadecimal digits in a byte)
  int n_hex_digits = 2 * (sizeof n);
  char *string = malloc(n_hex_digits + 1)

  // print hex digits from most significant to least significant
  for (int which_digit = n_hex_digits - 1; which_digit >= 0; which_digit--) {
    // shift value across so hex digit we want is in bottom 4 bits
    int bit_shift = 4 * which_digit;
    uint32_t shifted_value = n >> bit_shift;
    
    // mask off (zero) all bits but the bottom 4 bits
    // 0xF is (1 << 4) - 1
   	int hex_digit = shifted_value & 0xF;
   	// hex digit will be a value 0..15 corresponding to the ASCII value "0123456789ABCDEF"
    int hex_digit_ascii = "0123456789ABCDEF"[hex_digit];    
    string[which_digit] = hex_digit_ascii;
  }
  string[n_hex_digits] = 0;
  return string;
}
```









