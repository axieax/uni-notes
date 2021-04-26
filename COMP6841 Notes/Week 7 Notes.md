



# Extension: Rootkits

- Root - god user of Linux systems (id=0)
- Malware/ransomware able to bypass any restrictions - extract more data / modify data
- Rootkit - tool designed to let you keep root and often hides the presence of an attacker
  - Hides processes/files/network traffic
  - Might have a built-in backdoor
  - Survives reboots
- Types
  - Userland (what you see when you run a computer)
    - Common on Windows - dll (replace with malicious code)
    - Unix: probably consists of multiple files
      - Overriding system library files (libc.so)
        - Modify e.g. if file == malware return file not found, else open()
      - Replacing common utilities - e.g. ls not showing hidden directories, netstat not showing a certain port, ps hiding process
    - Can infect important processes such as sshd
  - Kernelland
    - Often has a userland part - kernel code is difficult
    - Kernel runs in ring0 (can access everything and execute any instruction), userland in ring3
    - System calls is how userland programs talk to the kernel (array of function pointers to very important functions - very easy to hook)
      - Most common use is filtering data coming back to user - e.g. hide files, ports
      - Can also implement backdoors - if open a certain file or a file exists, give root
    - Kernel rootkit
      - Hooking functions in kernel land
      - Goal to hide stuff, often through replacing common syscalls
      - Difficult to write and detect - can't trust operating system
      - Malware can use this rootkit to help hide, gain privileges etc.
      - Usually a tool for an attacker - long game
  - Hypervisor
    - Runs at ring -1 (used when running a kernel as a virtual machine)
    - Runs between os and hardware, acting as a Virtual Machine (VM) monitor (used to manage OS)
    - Can infect parent machine (through VM) and other VM's as well
- Usually needs root to install
- Hooking (hiding)
  - Goal: redirect code execution
  - Finding where to hook is important
  - Actual code - overwrite instructions with a jump to malicious code
  - Array of function pointers - replace an entry or hook the entire table
- Interrupt Descriptor Table
  - Interrupt
    - Going from user to kernel (old syscalls)
    - Page fault
    - Division by zero
    - etc.
  - Another array of function pointers
  - Can hook more high level stuff - e.g. syscall table handler and page fault handler
  - Can be found with the sidt instruction - stores the IDT as a register
- Detecting:
  - Userland
    - Quite easy to detect in some cases
      - ex: overwriting common programs (ls etc.)
        - Compare hash of software with top 1000 program signatures
        - Have signatures for all your binaries/dlls/config files
  - Kernelland
    - Anomaly detection of pointers (e.g. syscall table not ordered)
      - e.g. sys_call_table[219] = c017aa70, sys_call_table[220] = <u>d0834000</u>, sys_call_table[221] = c019d950
    - High vs low
      - ls a directory, then parse it on disk. Compare the results.
    - Look for structures that you just can't hide
      - Can't hide open network connections completely.. (computer knows to read data from it)
    - Kernel can access all of memory - look for signs of malware/rootkits in memory
      - e.g. signature common malicious functions (e.g. setting user to root - unlikely to be in normal kernel)
    - Usually requires you to write kernel code
    - `/dev` list of all devices
    - `/proc` list of all processes (e.g. `/proc/kallsyms` kernel functions with sequential addresses)
    - Type 1 and Type 2 errors
      - Previously discussed modifying kernel structures that aren't meant to be changed (e.g. syscall table), allowing for easy detection
      - Type 2 change things that are meant to be dynamic
        - Modify internal kernel structures on the heap
        - Direct Kernel Object Manipulation (DKOM)
      - Type 2 ex: add a kernel module and remove it from the linked list of kernel modules
- *_ops (operation) structure
  - Dynamic
  - Different struct for different directories (e.g. proc, dev, usb)
  - Can be hooked and difficult to detect - can be anywhere in memory, hard to control what they are meant to be (meant to be dynamic)
  - Better than hooking syscall table (changes to static file can be easily detected)
  - Directly modify syscall in IDT instead of sys_write in syscalls table etc.
- Virtual memory hooking
  - Memory hooking by modifying page tables (arrays of pointers to real memory) which maps virtual addresses to physical addresses
  - e.g. for processes such as anti-virus, swap out memory corresponding to bad code with nothing, or good code (disguise)
  - Hook page fault handler to hook actual memory (page faults were an interrupt)
  - Replace the page fault handler with malicious one
  - Page out the chunk of memory we want and replace it with malicious
  - When a process requests access to that page of memory, lie and give it back a different part of memory
- ssh based on a config file - can be modified for a backdoor

# Tutorial: Case Study 7: Problem

- Mission duration near 6 days
- Last minute crew change - sickness vs practice
- Little interest in "routine" mission until incident occured
- Issue with routine cryo stir for the oxygen tank, where the damaged wiring inside ignited an explosion causing an oxygen tank explosion
- Many issues - required improvisation - change goal from landing on the moon to getting the astronauts back to Earth safely
  - Limited oxygen
  - Limited power
    - Shut down computers
    - Simulation on Earth for starting computer with only 20 amps of electrical current available
    - Manual manoeuvre of the rocket
    - No waste disposal
  - Excessive carbon dioxide
    - Improvised a mechanism from simulating available resources on the rocket
  - Cold - inedible food, lethargy from lack of sleep
- Teamwork both on the rocket and back on Earth
  - Failure is not an option
  - Relentless determination for solving seemingly impossible challenges - "you need a break?" "If they don't get one, I don't get one."
  - Communication is crucial
  - Running simulations on Earth with conditions on the rocket to try to come up with feasible solutions
  - Checks of references from multiple sources for calculations
  - Prayers from around the world
- Changes
  - Another cryo oxygen tank that could be isolated to only supply the crew.
  - Removing all cryo tank fans and wiring.
  - Removing the thermostats from cryo tanks, and changing the type of heater tube.
  - Adding a 400-amp-hour lunar module descent stage battery.
  - Adding water storage bags to the command module.
  - [Apollo 13: Facts About NASA's Near-Disaster | Space](https://www.space.com/17250-apollo-13-facts.html)

- Decentralised control
- Conflict of interest
- Communication



Past Exam

bits of security for passport photo

bits for each identifiable feature - e.g. eyes colours, face shapes etc.

People change appearances over time - multiply by 4 etc.

b64 instead of jwt for dict - too long

# Week 7 Reflection

This week's topic on authentication and data was very interesting. I enjoyed exploring different methods of authentication and protocols which I have heard a lot about before, although not exploring in too much detail, such as S/Key, TOTP, HOTP, OAuth and 2FA. Learning about the authentication attacks was also very interesting, since I have just blindly accepted these protocols to be secure before. Learning about data breaches and the importance of protecting data was also quite interesting. Completing activities on this topic allowed me to further explore how the GDPR relates with this principle. Furthermore, in this week's tutorial, we explored Case Study 7: Problem, discussing the Apollo 13 incident, specifically what went wrong and methods of preventing a future disaster from happening. Since I was well prepared, I had a lot to discuss and got a lot out of the case study, such as some of the security concepts which I had missed in my own analysis. I also found this week's activities very interesting, where I was able to explore many topics I am interested in, such as iPhone security, and learning more about authentication protocols and the Chinese Social Credit system. Through looking at what others have also learned from the activity, I gained a wider understanding of the Chinese Social Credit system and some of its security concerns which I had not considered before, such as the direct impact on their opportunities for travel and for their children as well. 

