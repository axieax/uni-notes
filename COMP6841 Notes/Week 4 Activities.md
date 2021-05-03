# Community

## Security Everywhere

## BonziBuddy, an Insider

BonziBuddy is a multi-purpose desktop virtual assistant which could perform tasks such as sharing jokes and facts, managing downloads, singing songs and talking to the user. Not only was it infamous as one of the most annoying apps to have ever been created, but was also controversial in its secondary role of being spyware and adware. This example of a trojan horse can also be thought of as an insider attack, where it was originally widely used and trusted as a desktop assistant by many individuals until it was discovered to have a malicious payload. This meant that it was able to infiltrate a computer as an insider and avoid detection for its malicious payload. As such, lawsuits were filed against it in 2003 due to the misleading nature of its software, causing it to be discontinued in 2004. Although the website was up until 2008 so the software could still be downloaded, the servers have been taken down a long time ago so the spyware part of the program is finally redundant. 

![Bonzi Buddy.png](https://upload.wikimedia.org/wikipedia/en/thumb/9/9d/Bonzi_Buddy.png/300px-Bonzi_Buddy.png)

# Foundations - Secrets

### Our Own Slip-ups

What corruption? Fake news!
https://www.openlearning.com/u/axie/blog/OurOwnSlipUps/

Moving to a new primary school in year 5, I was tasked with helping develop the school's IT infrastructure after several teachers noticed my proficiency with solving technical issues for both my peers and teachers. After helping solve several major issues regarding faulty Internet connections and student laptop setup, I was trusted enough to be given administrator privileges as an insider. As someone with inherently strong morals, I knew better than to abuse my power.. too much. I was also quite a troll back then, and enjoyed pulling pranks on my friends, such as disguising a shutdown script behind an Internet Explorer shortcut, or remotely shutting down a friend's laptop or displaying tons of annoying popups and windows just to mess with them. Although these were just innocent pranks back then, I realised that there was definitely potential for corruption and major internal damage, especially if I could go back in time with my current level of technical knowledge. However, being more mature, I am less likely to even pull pranks on my friend, unless they explicitly express their permission for them, as per the Good Faith Policy. 

# Security Engineering

### Merkle Puzzles

1. Pick an envelope at random and brute force all possible letters till you crack it and it opens
2. Enter your secret message into the **Plain Text** box at the bottom of the opened letter.
3. Your encrypted message will be shown in the Cipher Text box - copy all of it and paste it into a comment below.
4. Crack at least two other students' messages from different envelopes by trying envelopes one at a time till you find theirs, and then posting their ciphertext into the cipher text box - their decrypted message will appear below in the plaintext box. Done!
5. Reply to the two students using their code key in their envelope - you now have a (somewhat) secure channel with them.
6. Log what you did and your reflections in your blog.

Picked envelope #11 - Key brute force decrypted with B

**Message Identifier** : potato

**Key** : C6359B3CA22B557C87127B78F63B7105

- 5: cheese
- 6: fierce
- 7: cats
- 8: cow
- 9: golf
- 10: pizza

[Jefferson Zheng](https://www.openlearning.com/unswcourses/courses/sec-21t1/activities/merklepuzzles?inCohort=unswcourses%2Fcourses%2Fsec-21t1%2FCohorts%2FClassOf21T1#comment-604de2f5ab8f0b0c06d5b460):

I used the pizza key : FjJZZVNbL2lUUyYnEjZQNjJbVEIdYkRBVFVYUFpmQlc3JlNpOFsmMEJDICQeZlIqI1dCVB1iR1hSXV1URWoRWSwsWStBFywqFldjMlc1UC8jEkJUVCYXU0RYHw==

Envelope 10

Two all-beef patties, special sauce,
lettuce, cheese, pickles, onions on a sesame seed bun.

dO yoUr bIg mAcS cOmE iN vEgaN?!?!?! (JgoWPF1iMWRUfyRhXwdSEWZRflx0Yl5/EUB0VlcIDhd9ZAlk)

[Jamison Tsai](https://www.openlearning.com/unswcourses/courses/sec-21t1/activities/merklepuzzles?inCohort=unswcourses%2Fcourses%2Fsec-21t1%2FCohorts%2FClassOf21T1#comment-604e2394fac5093969b3b6af):

I used the cats key : exB9LV9dYxFSUSRfJkEY

I Like Waffles! (exBVK1ofN2ZfXilWY0VYIlMoXEE=)



For this activity, I randomly chose Envelope #11. Brute-forcing the key for this envelope was very quick. Starting from the beginning of the alphabet, the second letter, B, managed to reveal the message identifier "potato" and the key "C6359B3CA22B557C87127B78F63B7105". Using the encryption utility, I was able to quickly generate the following ciphertext message to be sent: I used the potato key : KhZfWk8nEyAuX0J0DQEGYxkGEAMWcxYJZwcScw==

For cracking other students' messages, I decided to try the middle four squares as I thought these would be the most common ones despite a random choice (also why I chose Envelope #11). I first tried cracking [Jefferson Zheng](https://www.openlearning.com/unswcourses/courses/sec-21t1/activities/merklepuzzles?inCohort=unswcourses%2Fcourses%2Fsec-21t1%2FCohorts%2FClassOf21T1#comment-604de2f5ab8f0b0c06d5b460)'s cipher text which used the pizza key. I decided to note down failed attempts of getting the right key as well, which would help me later on for cracking another cipher text. Since I only wanted to try the middle four squares first, I was able to find the key on my third attempt, each attempt also involving some brute-forcing for the single alphabet key. Now that I have obtained the key corresponding to the pizza cipher, I was able to decrypt his message and reply with another one using the same key, without having to reveal the message identifier anymore. [Jamison Tsai](https://www.openlearning.com/unswcourses/courses/sec-21t1/activities/merklepuzzles?inCohort=unswcourses%2Fcourses%2Fsec-21t1%2FCohorts%2FClassOf21T1#comment-604e2394fac5093969b3b6af)'s key used the cats message identifier, which I had already noted down as being in Envelope #7. Knowing this, I went back to that envelope and since I had a good memory, remembered the key was "W" (my brain somehow associated that letter with cats I guess) and immediately got the corresponding key. Using the same process, I was able to start a (somewhat) secure channel with him as well. 

Honestly, I thoroughly enjoyed completing this activity as it uses a very interesting and interactive way of showing how Merkle puzzles can be used to start a somewhat secure channel between two users for smaller complexities. It also shows how once a hacker has brute forced their way to obtain the key, everyone's messages in the channel can be decrypted, where I was able to read other's messages in the same message thread after finding the key. Brute forcing with larger numbers of envelopes and key sizes can easily get very complex, which could have been more emphasised if other students didn't use the shortcuts that I did. Even though a computation can brute force much faster than humans manually, cracking would still take quite a long time for large complexities. 

### Learn how RSA works

I really enjoyed completing this activity as there were many concepts from Discrete Mathematics which I enjoyed doing, such as modular arithmetic. Seeing its applications in cryptography is very interesting. I used Python's pow() function to complete the Modular Exponentiation task, since my wifi was very slow and I couldn't be bothered waiting for Wolfram Alpha to load. For example, $28^{267} (mod 21)$ can be calculated with `pow(28, 267, 21)`.

Calculting Modular Multiplicative Inverses using guess-and-check (brute force) and the extended Euclidean Algorithm was something I have not done for a long time, but I remembered how to do them after a quick glance over my Discrete Mathematics notes. My working can be found in the image below.

<img src="images/mod working.jpeg" alt="mod working" style="zoom:50%;" />

I wrote a Python program (below) to help me solve the RSA exercise. Although I didn't initially understand how the algorithm worked when studying Discrete Mathematics, I am now quite confident with understanding how the encryption and decryption processes work. I found the process of representing a string as a number which can then be transformed mathematically very fascinating as well, emphasising the close relationship of mathematics and computer science (my degree!!).

```python
import re

# Plaintext
plaintext = 'RSA'
print(f'Plaintext: {plaintext}')


# Encode
print('=== Encode ===')

# Convert each character in string to a two-digit number
encoded = []
for c in plaintext:
    val = str(ord(c) - ord('A') + 1)
    encoded.append(val if len(val) > 1 else '0' + val)
encoded = int(''.join(encoded))
print(f'Encoded plaintext: {encoded}')


# Encryption
print('=== Encryption ===')
e = 7825
N = 467323

# encrypt x using x^e mod N
ciphertext = pow(encoded, e, N)  
print(f'Encoded ciphertext: {ciphertext}')


# Decryption
print('=== Decryption ===')
d = 214833

# decrypt y using y^d mod N
decode = pow(ciphertext, d, N)
print(f'Encoded plaintext: {decode}')


# Decode
print('=== Decode ===')

# regex to get two characters at a time and decode to get plaintext
decode = [chr(ord('A') + int(x) - 1) for x in re.findall(r'..', str(decode))]
plaintext = ''.join(decode)

print(f'Decoded plaintext: {plaintext}')
```

### Symmetric









# Extension

## Format String Wargames

After rewatching the webinar several times to make sure I understood everything, this activity didn't turn out to be too difficult.

### Wargame 1: Easy

The flag COMP6447_ADMIN can be uncovered with a simple `objdump -s -j .rodata ./easy`.

### Wargame 2: Medium

For this challenge, I used `info variables` after running gdb on the binary file to find username at 0x0804a060 and password at 0x0804a0a0. Brute forcing using pwntools to find an offset for a %offset$s format specifier, I found that an offset of 14 bytes gave the output b'Enter Username:\nAAAA41414141\nInvalid Username\n', which means that AAAA can be substituted for a valid memory address to be accessed. From this, I tried `python -c "print '\x60\xa0\x04\x08%14$s'" | ./medium`. After 2 hours of debugging, rewatching the webinar and stack-overflowing, a classmate said to try flip the quotation marks around to `python -c 'print "\x60\xa0\x04\x08%14$s"' | ./medium`, which allowed me to get the flag TOPSECRETPASSWORD for the password.

username: COMP6447_SUPER_SECRET_ADMIN

password: TOPSECRETPASSWORD

Can also get address from observing stcmp call using objdump -d medium

### Wargame 3: Chained

From running this program, I figured out that two random variables generated would be stored somewhere, whose sum is then computed to check for a sum match from the user. Using the same method as before, I found the variables random1 at 0x0804a080 and random2 at 0x0804a088, and an offset of 13 bytes when brute forcing one of the variables. From this, I crafted the command `(python -c 'print "\x80\xa0\x04\x08\x88\xa0\x04\x08%13$s %14$s"' && cat) | ./chained`, using `&& cat` to make the process interactive and prevent it from exiting after piping input into it ([source](https://stackoverflow.com/questions/5843741/how-can-i-pipe-initial-input-into-process-which-will-then-be-interactive/5852578#5852578)). I then manually added the numbers together and got the flag ENROL_IN_COMP6447.





Find offset without Python:

`for i in $(seq 1 30); do echo "Offset $1"; echo "AAAA%$i"'$x' | ./medium; done | grep 41 -C 2`





