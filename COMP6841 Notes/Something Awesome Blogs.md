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





