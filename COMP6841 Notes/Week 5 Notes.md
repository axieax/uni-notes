# Monday Lecture

Cryptographic Hash Function Properties:

- Pre-image resistance - one-way function (difficult to find input given output)
- Second pre-image resistance - given an input, difficult to find another input which gives the same hash
- Collision resistance - 



Birthday Attack



# Tuesday Lecture

# Extension: Forensics

Optical hard drive data forensics:

- Data written sequentially, slow random
- File deletion - marked as deleted - data isn't wiped
- Byte for byte copy (see everything on hard drive) vs logical file extraction (what's visible to the user)
- sudo mount to mount dump
- Can find deleted data using ghex
- Magic bytes for different file formats (header and footer) for file command
  - scalpel to grep for magic bytes
- shred -u to overwrite and completely delete

Network forensics:

- Wireshark
- IP Addresses, User-Agent (in HTTP), Accept-Charset (device), Time to live (device), Header checksum (man in the middle attacks might forget to change this)
- Protocols - TCP, SYN, ACK, FIN, HTTP

 

strings

# Tutorial: Case Study 5 - Snoop

Government surveillance

- Pros
  - Safer society (opportunity cost) - can catch often missed warning signs (e.g. mental health?)
    - e.g. mobile phone detection cameras, criminal network monitoring
  - Centralised authorisation and convenience - e.g. facial recognition technology replacing Opal cards and other tickets, contactless payments, building entry
- Cons
  - Backdoors required - breaks how encryption works - systemic weakness
  - Data may be invalid or inaccurate - e.g. mobile phone detection cameras using AI - no 100% confidence - more court cases / appeals
  - Relies on trust in gov
  - International laws - monitoring of data stored overseas? who has legislation?
  - Spyware can be compromised / potential massive data leak
    - foreign countries having access to everyone's data
    - valuable data to individuals (hackers) and companies
  - Difficult to have an opt-out system when everyone will be scanned / monitored
  - Increased risk of blackmail, discrimination and persuasion
  - Mass government surveillance can be a slippery slope for privacy
  - Can ironically cause a lack of identity
  - Necessity of surveillance?

Privacy of citizens

- Pros
  - No secrecy / privacy - constantly live in fear
  - “People have a right to expect a certain level of privacy when navigating public spaces, and must have trust that governments are taking appropriate action to protect that privacy.” - Tim Singleton Norton, the chair of Digital Rights Watch
  - Intellectual privacy
  - Data leaks
- Cons
  - Corporate access to data can be very harmful
  - Greater societal benefit?

Additional points:

- Freedom of speech
- Insider government attack
- Welfare
- Constitution
- Type 1 / Type 2 Errors



# Weekly Quiz



Q5

- 60 bits of output
- Birthday attack - 30 bits for expected value of hashes before first collision
- Work for first collision - 50 bits (since 20 bits required for each hash)
- Let P(BF) be the probability that one page begins with banana and the other page begins with fish
  - Assume that for a lower bound, there is an average of 3000 characters per page with 94 different combinations for each character (keyboard: 52 letters + 42 numbers and symbols). This means there are 94 ^ 3000 combinations of pages.
  - Let P(B) be the probability that a page begins with banana and P(F) be the probability that a page begins with fish. Since these are independent events, P(BF) = P(B) * P(F)
  - P(B)
    - Fixing the first six characters, there are 94 ^ 2994 ways to choose the remaining characters.
    - Thus, P(B) = 94 ^ 2994 / 94 ^ 3000 = 94 ^ -6
  - P(F)
    - Fixing the first four characters, there are 94 ^ 2996 ways to choose the remaining characters.
    - Thus, P(F) = 94 ^ 2996 / 94 ^ 3000 = 94 ^ -4
  - Thus, P(BF) = 94 ^ -6 * 94 ^ -4 = 94 ^ -10
  - If there is a 94 ^ -10 chance that one page begins with banana and the other with fish, there are therefore 65.5 bits of page combinations required to get close to guaranteeing this outcome. Even considering half of these bits on average would mean the number of bits required would be closer to 70 due to the lower bound. 
- Hence, 120 bits required

^ Incorrect

sqrt(60 bits) => 30 bits

20 bits for each

50 bits

Then doubles for fish and banana





