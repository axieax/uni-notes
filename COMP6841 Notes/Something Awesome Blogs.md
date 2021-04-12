# Something Awesome Blogs

## Proposal

**Chrome Credential Stealer**

For my Something Awesome Project, I'm thinking about writing a program which steals saved user credentials from Google Chrome, a popular browser used by many. Since the saved credentials have to be stored somewhere and recovered later for functions such as autofill, I figured that although the passwords are most likely encrypted, they are probably reversible so they can be retrieved in the future. Doing some research, I found out that these credentials are stored in a SQLite database, with passwords encrypted using the AES-128-CBC standard. However, accessing the database on later versions of MacOS may be a bit more difficult, requiring the user to enter their password in order to access the safe storage key. As such, I'm looking to find ways to bypass this restriction or try to get a user to enter their password through social engineering. Of course, all this will be done with their explicit consent beforehand, although being aware of the true purpose of the program will cause confirmation bias in testing so I'm thinking of splitting my testers into two main groups:

1. Testing program compatibility and successful extraction - explicitly tell them beforehand about the credential stealer and promise (show in front of them) that their extracted data will be completely destroyed after the test
2. Testing social engineering - modify my program so that instead of sending off their credentials, the extracted credentials are displayed on their screen or stored locally on their devices for them to confirm and delete at will

I'm planning on programming this in Python, with different levels of execution from running the script manually, hiding it inside another application or browser extension as a trojan, or through a USB. Encrypting and sending the extracted data to a remote server will also be the most convenient method (or to a local server. This will definitely be a challenging project and I hope to learn more about password security from this exercise. 

**Topics covered:**

- Internet and computer security
- Reverse engineering
- Encryption / decryption
- SQL database access
- Trojan programming
- Social engineering
- Operating systems

**Success criteria:**

- Pass
  - There is evidence of a correct logical thought process for solving the problem, and database on Windows successfully accessed to retrieve encrypted credentials (with encrypted passwords)
  - Poor code formatting
  - Includes a supporting article / documentation for the project
- Credit
  - Partially working on Windows only
  - Extracted (decrypted) credentials displayed on Python output only
  - Ok code formatting
  - Single executable Python script visible to the user
  - Includes a supporting article / documentation for the project
- Distinction
  - Partially working on Windows, Linux
  - Extracted (decrypted) credentials saved to a file
  - Good general code formatting
  - Attempted to hide code execution from the user
  - Includes a supporting article / documentation for the project, discussing Chrome's password encryption methods
- High Distinction
  - Working on Windows, Linux, MacOS
  - Extracted (decrypted) credentials sent to a remote server
  - Well-formatted code with concise explanations
  - Code execution hidden from the user, using social engineering to gain additional permissions if required
  - Includes a supporting article for the project, discussing Chrome's password encryption methods and comparing with other common browsers such as Firefox, Edge and Safari

<u>Links to check out:</u>

- https://steveperrycreative.com/post/how-chrome-stores-your-passwords-windows-and-macos-and-why-you-still-shouldnt-let-it

- http://raidersec.blogspot.com/2013/06/how-browsers-store-your-passwords-and.html

- https://source.chromium.org/chromium/chromium/src/+/master:components/os_crypt/os_crypt_mac.mm (Chromium source code in C++ / Objective C)

- https://docs.ioin.in/writeup/bufferovernoah.com/_2016_10_17_chrome_/index.html



## My final PC part has arrived - time to start my project!

My CPU arrived today, which was surprising since Amazon said the expected delivery was on the 23rd of March. I wanted to assemble my PC as soon as possible so that I could start on my Something Awesome project. Because of the heavy research I have conducted over the last several weeks, I was quite ready to start "hacking" my own Chrome installation and writing my exploit in Python. Although my Wifi was non-functional, which meant installing Windows, Drivers, Chrome and setting up a development environment on my Windows took way longer than expected, I was still able to make much progress in a short amount of time using my mobile data. Once I located Chrome's credential storage database and started to play around with it, I was able to successfully extract encrypted credentials soon after. I used [SQLi attacks](https://github.com/axieax/chrome-credential-stealer/blob/59c41357f58efb2138198f2ab093b64ed16d9662/windows.py#L22) learned from the course to learn more about the SQLite database, before I was able to [extract the credentials I wanted](https://github.com/axieax/chrome-credential-stealer/blob/ffdc6a8e75ce4413767a4bf5341ce7748d5cd275/windows.py#L20). Although I ran out of time for the day, having done the research, I knew that all I have to do next is to use pywin32 to decrypt the passwords in order to complete the Windows exploit and secure myself a passing mark. However, of course I am going to aim for the higher marks detailed in my proposal. 

# Reflection

Looking back at the amount of work I've done for my Something Awesome Project was quite frightening where I spent around 120 hours in total as I challenged myself to learn more about the subject I love learning about. However, my efforts have been extremely rewarding, where I was able to produce an end product that I was extremely proud of: my remote program as well as my detailed 4000-word writeup on the project. I have been able to apply several of the concepts learned from the course, as well as learn many interesting topics on my own. In my proposal, I detailed my plans of making a Google Chrome credentials stealer for Windows, macOS and Linux. However, over the course of the project, I realised that I was more interested in developing a stealer for a wider range of data from a wider range of supported Chromium browsers since there doesn't seem to be a similar tool available yet, and I was interested in seeing how these data can be used to build a profile for a user. Implementing the local extraction process for KrwmTools easily took more than 50 hours, with many hours spent looking over the Chromium source code in an attempt to reverse engineer the encryption process for passwords. In hindsight, learning more about the AES-GCM cipher once I had found out which specific cipher was used would be helpful in understanding the relevant concepts sooner. However, my initial research on Chrome data encryption was offsetting and contradictory to 

However, I was determined to keep going and implement a feature to send the extracted data remotely, which was one of the reasons why I wanted to do my credentials extractor project in the first place. This part also took way longer than expected since I kept trying to challenge myself to come up with a secure and effective protocol. As mentioned in my writeup, I was able to implemented a HTTP connection to a Flask server using the requests library in a few minutes. However, I challenged myself to use a defender mindset to design a secure way of sending the extracted data from a client to the server, from just using RSA encryption to a hybrid RSA and AES scheme due to the slow performance and restrictions of RSA for large data. I also learned more about general networking (IP addresses and protocols like TCP) through learning about socket programming. 



Topics covered



Went beyond my initial criteria

Apply many concepts learned from course

Rewarding

Good faith policy









