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

Thinking about the amount of work I've put into my Something Awesome Project was quite frightening when I realised I've spent around 120 hours in total as I constantly challenged myself to learn more about the subject I love learning about throughout the process. It was indeed quite a rewarding experience, however, where I was able to consolidate my knowledge regarding several of the concepts learned throughout the course, such as SQL injection, cryptography and cyber security, applying them to produce an end product that I am extremely proud of - my remote KrwmTools extractor program as well as my detailed 4000-word writeup on the project. My initial proposal described my plans of making a Google Chrome credentials extractor for Windows, macOS and Linux. However, over the course of the project, I realised that I was more interested in a developing an extractor for a wider range of data from a wider range of Chromium browsers as there doesn't seem to be a similar tool available yet, and I was interested in seeing how these sensitive data can be used to build a profile for a user. 

Implementing the local extraction process for KrwmTools easily took more than 50 hours, with many hours spent analysing the Chromium source code in an attempt to reverse engineer the encryption process for passwords. In hindsight, taking the time to learn more about the AES-GCM cipher once I discovered that that was the cipher used to encrypt the data would be very helpful in understanding the relevant concepts and terminologies sooner, such as nonce and authentication tags. Furthermore, my initial research on Chrome data encryption added a layer of confirmation bias to my search for the DPAPI function used to encrypt the data, before I came across an article mentioning that Chrome had changed its encryption method after version 80 (as stated in my writeup). Nonetheless, reverse engineering the source code was an interesting and rewarding experience that forced me to consolidate my understanding of concepts such as AES encryption and operating systems (specifically Windows) in order to successfully complete the first part of my project. 

Although I had already spent a lot more hours on this project than anticipated, I was still determined to keep going and implement a feature to send the extracted data remotely, which was one of the main reasons why I wanted to my initial credentials extractor project in the first place. However, I ended up taking just as much time in the second part as the first part, even though I was able to set up a HTTP connection to a Flask server using the requests library in only a few minutes. Noticing that this slowed down my client-side extraction script quite a lot, I looked into socket programming which was one of the topics I wanted to learn about anyways, allowing me to improve my understanding of computer networking in the process, such as the TCP protocol and IP addresses. I then further challenged myself to switch to a defender mindset and implement a secure method for sending the extracted data from a client to the server, which I did not consider in my original proposal. From what I learned in the course, encryption with the server's private RSA key made perfect sense here, as the data can only be decrypted directly on the server knowing the corresponding private key. However, I found that in practice, RSA encryption was not ideal for large data, involving breaking the message into blocks and a very slow decryption time. After doing a lot of research, I decided to implement a hybrid encryption scheme which brings the efficiencies of symmetric AES encryption and decryption for data to be sent across the socket, with RSA enabling the key exchange. Through this experience, I realised the importance of considering multiple solutions in security, seeing how some solutions can be combined to make one that can satisfy my criteria for a secure yet efficient method. 

Synthesising my several pages of notes over the last 8 weeks and explaining all my topics in a concise manner was a challenge I encountered during the writeup process. However, I was able to produce a writeup that detailed my thought process throughout the project, explained relevant concepts appropriately and demonstrated the hours I put into research for this project. An interesting part of this experience included reading academic papers to evaluate the AES-GCM cipher in order to ensure my socket encryption was secure, which caused me to go back over my code and update my implementation accordingly (please see the second last paragraph in part 1.2 of my writeup). I also learned more about cyber security as I investigated ways of improving Chromium encryption involving alternatives for storing encryption keys locally, such as password managers and other methods of authentication. Although the entire project took way longer that expected, I really got out what I put in and enjoyed learning more about security in the process. I definitely went beyond the criteria I had initially set for myself, as evident in the performance of my program as well as the detailed writeup. Since my project involved remote spyware, I had to be considerate of ethical concerns and practise professional behaviour throughout the project. I split my main testers into two groups, with one group testing that their Chromium data could be extracted locally and the other testing that a socket communication could be successfully established remotely. I was able to combine the results of both groups to demonstrate remote data extraction, which I had only tested over my own computers as well as my parent's, who gave me explicit consent to do so. 







