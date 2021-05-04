TLS Wireshark Analysis: https://youtu.be/MQg48n9lV0s

# Extension: Reverse Engineering

- Uses:
  - CTF fun
  - Bug bounties
  - Corporate espionage (stealing technologies)
  - Malware analysis
    - Neutralise malware e.g. wannacry kill switch (unregistered web address) found from reverse engineering malicious code
    - Improve security - understand exploit in order to defend against it
    - Improve malware
  - "Extend" the functionality of software
  - Interoperability ("extend" the function of software you own)
  - Security audit closed source software
- Example compilation
  - Preprocess only: `gcc -E -O0 -fno-stack-protector example1.c > pre.c`
    - E: preprocess only (replacing #include, macro sub)
    - O0: Don't optimise
    - fno-stack-protector: no stack protection (buffer overflow etc.)
  - Compile only: `gcc -S -O0 -fno-stack-protector example1.c`
    - To assembly, default x86
  - Assemble but don't link: `gcc -c -O0 -fno-stack-protector example1.c`
  - Link: `gcc -c -O0 -fno-stack-protector example1.c`
  - Do everything: `gcc -O0 -fno-stack-protector example1.c`
- What to do (static analysis - examining binary without executing)
  - Disassemble from machine code to assembly
    - Does not guarantee original assembly, hopefully close enough (similar to translation, A -> B and then B -> A)
    - On CISC platforms with variable-width instructions, more than one disassembly may be valid. This is also true on RISC architectures but less frequent.
    - Disassemblers do not handle code that varies during execution
    - Static analysis tools
      - Cutter - Hexdump, Strings, Disassembly, Graph (control flow), Decompiler (Ghidra, r2dec)
      - Ghidra
      - Binaryninja (paid, free demo)
      - Radare2
      - Ida (paid, free version)
      - Hopper
  - Decompile
    - Attempts to create source code that matches the function of the provided machine code
    - Does not guarantee original source code
- Tips
  - Look at the big picture - don't get caught in the assembly
    - System calls
    - Control flow
    - Look at strings
  - Only focus on things you are interested in (going backwards)
  - Try to get familiar with the program beforehand by running it
  - Might be compiled with debug symbols, e.g. Diablio with debug symbols contained in 'DIABPSX.SYM' and rich header in executable detailing the exact version of the original compilers and linkers used
  - Might also have partial/full source code leaks
- Dynamic analysis - using debugger (e.g. gdb) during execution



# Tutorial: Case Study 8 - Ghost

Communication and trust through an untrusted third party

Major establish protocol which Nick does not know, or questions

Codewords, ciphers

Some way to implement a message authentication code or hash, encrypt



Relying on alien to communicate - single point failure













