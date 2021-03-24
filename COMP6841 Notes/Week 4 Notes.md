# Monday Lecture





# Tuesday Lecture

Walls - many examples of walls as defence - many other ways of attacking them, single point of failure, false sense of security (defence in depth - reliance on walls - postponing the inevitable can be worse)

Motive - the more you think they're acting in your interest, the more you think they're selfless, the more you trust them

Insider attack

- Reasons: whistleblower (think they have a moral reason), greed, hate the company/personal reasons, informant, idiot, blackmail
- Defence: detect the insiders, expel the insiders, least access privilege, encourage people to report traitors, separation of powers

People often go after whistleblowers / people who leak info about them - angry

Human weakness - corruption and self interest (or conflict of interest)

# Extension: Format Strings

```c
// demo
char *secret = "secret message lol";

int main() {
  char buffer[512];
  fgets(buffer, sizeof(buffer), stdin);
  // printf(buffer);   -- would be vulnerable if %s in buffer
  printf("%s", buffer);
}
```

General:

- printf() and vprintf() write output to stdout
- fprintf() and vfprintf() write output to the given output stream
- sprintf(), snprintf(), vsprintf() and vsnprintf() write to the character string str
- %s - print array of char.. aka a string - tries to dereference address
- %c - print single char
- %d - print integer
- %p - print pointer
- %x - print hexadecimal
- %n - write the number of characters written so far into the integer pointed to by the corresponding argument (e.g. length of input string into argument variable) - can overwrite memory

## printf("%s", input);

- Arguments placed in reverse order, before format specifier (on descending stack)
  - moves address of 'input' string onto the stack
  - moves address of format specifier (%s) onto the stack
  - printf called in order

## printf(input);

- moves address of 'input' string onto the stack
- nothing below this string, so you can unintentionally read other values on the stack by injecting a format specifier offset by some positions
- e.g. AAAA %4$x
- stack addresses may not be correctly aligned
  - AAAAAAAA%x %x %x may return a result like F4374141 41414141 41410000
  - padding with 2 bytes fixes this:
  - <u>XX</u>AAAAAAAA%x %x %x returns F437<u>5858</u> 41414141 41414141
  - Addresses stored in little endian format

Try first with AAAA %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x %x etc.. then get specific with offset

`echo 'AAAA%4$p' | ./intro` returns AAAA 0x41414141 -> AAAA can be replaced by a memory address you want 

e.g. `python -c 'print "\x60\x85\x04\x08%4$s"' | ./intro`

- writes memory onto the stack and accesses it directly (ignoring the format specifier with offset)

Getting address:

- Read all constant strings from Read Only Data Section
  - `objdump -s -j .rodata ./intro`
- Dynamically read strings whilst running the program
  - `gdb ./intro`
  - `x/s (char *)secret`
  - Leak particular information from stack -> maths to find out something else in the program -> write back into program and execute it (e.g. for functions)

Exploits can be chained together:

e.g. **First target address: 0x12345600**
Second target address: 0x12345604
Exploit: **\x00\x56\x34\x12**\x04\x56\x34\x12**%4\$s**%5\$s (however printing this will terminate straight away since it begins with a null byte)
-> **%6$s**%7$s**\x00\x56\x34\x12**\x04\x56\x34\x12 (two extra offset since format specifiers are first)
Explanation: by the time it hits the null byte, the format specifier instructions have already been executed - addresses already dereferenced



Uses: Code execution, memory access (leaking information, overwriting memory), dump entire process space

Real life example: sudo (2012)

# Tutorial: Case Study 4 - Witness

Lawyer X - Nicola Gobbo

- Former gangland barrister also a police informer
  - Corruption issue: lawyer gives police information about their own clients (violating legal professional privilege - keeps communication between lawyers and clients confidential)
- One of the youngest women ever admitted to the bar (1998)
- Notable during the gangland era in the early 2000s by representing a rogue's gallery of Melbourne's underworld
- Police tried to keep her name from public disclosure all the way to the High Court -> Royal commission into the police's handling of Ms Gobbo and other informers
  - Convictions or findings of guilt of 1011 people may have been affected by Victoria Police's use of Ms Gobbo as an informant
- https://www.theage.com.au/national/victoria/the-nicola-gobbo-lawyer-x-scandal-explained-20201124-p56hh9.html



Discussed Pros + Cons in a debate

# Weekly Quiz

Merkle Puzzles

https://www.youtube.com/watch?v=KpaRRkGgAvs

1 million messages, each consisting of a different 200 character english phrase and a different 80 bit Merkle key, each message encoded using a different 40 bit CDMF key.

Average:

- 500,000 messages on average (about 19 bits)
- CDMF decipher -> 39 bits on average
- 58 bits of brute force



# Week 4 Reflection and Something Awesome Update

Given how busy these two weeks were for me (please see my schedule from [last week's reflection](https://www.openlearning.com/u/axie/blog/Week3Reflection/)) and the late release dates for week 3 activities, I had quite a late start to my week 4 security content and activities. For lectures, I found that this week's course notes did not provide much detail so I ended up watching the live lectures at 2x speed. Although this corresponded to having more hours spent on the subject this week, I'm glad that I was able to understand the content and listen to some great examples such the wall analogy, which wasn't very well-documented in the student notes. In the future, I'm planning to read the course slides along with the notes, searching up concepts on Google which I don't understand or are missing from the notes. I enjoyed learning about encryption and decryption this week, as these concepts are very relevant to my Something Awesome project, which is why I've decided to prioritise my activities and do all of the security engineering ones. I've spent about an hour after learning about these methods in the lectures researching how Google Chrome encrypts user passwords using AES, and found a clearer separation between Windows and MacOS machines. The AES encryption requires a secret key, initialisation vector and encrypted password for decryption (will need to do more research to find out where these are located). It seems that Windows uses the CryptProtectData API which can be decrypted using the Python library pywin32, in contrast to MacOS's more secure method of using a safe storage key. I also found about the 2019 CStealer Trojan, which steals Chrome passwords and uploads them to a remote MongoDB database. I've manage to locate the [source code](https://malwr-analysis.com/2020/03/28/password-stealer-trojan-malware-analysis/) which I will analyse in future weeks. I'm expecting my final PC part to arrive soon so I can start playing around with Chrome files and start writing my script. Amazon expects this to arrive late next week (image in my [portfolio checkin 2](https://www.openlearning.com/u/axie/blog/PortfolioCheckin2/)) but I have a society road trip soon after so I'll try to do as much as I can before then, and work on it some more the following week (week 7). My project looks promising and I hope to produce a tangible product soon. 

I found this week's tutorial quite interesting, and enjoyed hearing my peers discuss legal perspectives I had not considered regarding the Lawyer X case, such as the potential loss of trust in the system due to a revelation of confidential intel, and discussing the duty of lawyers whether that is to protect their clients, to the court or to society. Another ethical consideration is whether lawyers defending criminals is the best for society, but as some peers mentioned, a rebuttal is that everyone should be entitled to a fair trial. I enjoyed the mock trial format which definitely encourages active discussion between students. Adjudicating both law students in our class on either teams was very interesting as well, making for an intense debate with great points delivered from both sides. Discussing the weekly quiz was also very helpful. My initial solution for the bits question was very similar to the actual solution, but I just substituted incorrect values. Hearing my fellow peers discuss very large answers to the problem made me worry about my method, which was actually correct. Next time I should be more confident with my answers.







