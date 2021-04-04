# KrwmTools

# Introduction and Rationale

For my Something Awesome security project, I decided to build a tool kit aimed at extracting sensitive data from Chromium browsers. My project was inspired by the [LaZagne Project](https://github.com/AlessandroZ/LaZagne), an open-source credentials recovery application which can be used to extract browser credentials as well as other passwords stored on a Windows, Mac OS and Linux computers. KrwmTools focuses on Windows machines, extracting credentials, autofill information (fields, profiles, addresses, names, emails, phone numbers), credit card information, cookies and history (search terms and web history) from the ten most popular Chromium browsers, which could help build a profile for the users on a compromised computer. As detailed in my initial proposal, I had originally planned to create a password stealer only for the Google Chrome browser, working on all three operating systems. However, I decided to shift my focus to building a multi-purpose tool after realising the potential of other sensitive data which could be extracted as well, especially since there doesn't seem to be a similar utility available yet (on Google at least). My project is split into two sections: extracting the data, and securely sending the extracted data to a remote server (optional spyware functionality). 

> Git repository for source code and packaged Windows executable available at [https://github.com/axieax/krwm-tools](https://github.com/axieax/krwm-tools)

# Part 1: Chromium Data Extraction

## Part 1.1: Locating and extracting the credentials data

Due to issues with my MacBook, I was only able to start the project once my last PC part arrived so that I could finally assemble my Windows machine. Keeping in mind that I had initially only planned to extract credentials from the Google Chrome browser, I was able to quickly identify where the sqlite3 database for Login Data was stored (in the %APPDATA% directory) and use SQL queries learned from SQL Injection Wargames in the extension course, to learn more about how the data was stored. I discovered that the database would be locked with the browser being open, so I had to operate on a copy of the database file as a compromise. I kept this feature in my production code so that the browser did not have to be closed in order to extract data, and as will be discussed later, certain browsers like the Epic Privacy Browser used temporary databases which would be deleted upon exiting the browser. 

The Python code below is an extract of the reconnaissance attack I used to gain more information about the database structure for Login Data. 

```python
def sqli_recon(db_cursor) -> None:
    """ SQL queries to learn more about the database structure """
    # To find tables
    db_cursor.execute("SELECT name FROM sqlite_master WHERE type='table'")
    print(db_cursor.fetchall())
    # Table of interest: logins

    # To find columns for logins table
    db_cursor.execute('PRAGMA table_info(logins)')
    print([row[1] for row in db_cursor.fetchall()])
    # Columns of interest: action_url, username_value, password_value
```

Upon extracting the rows corresponding to credentials, I was surprised to see values for the action_url and username_value columns stored in plaintext, especially those associated with credentials that I remember saving on my MacBook's Chrome application, which definitely indicated that I was heading in the right direction. Since I had only just set up my machine, I did not expect anything to turn up as I did not realise my credentials were also saved on my Google account, which is pretty convenient I suppose. 

## Part 1.2: Decrypting the data

As expected, the passwords were encrypted (thankfully!). From my research, it seemed that all I needed to do now was pass the encrypted passwords to Window's DPAPI (Data Protection API) for decryption, using the pywin32 Python package in order to make this Windows API call in Python. **EXPLAIN THE DPAPI AND EVALUATE**

However, once I had finally managed to install the dependency using another wrapper package (pypiwin32), I knew something was wrong when the passwords could not be decrypted using this approach. 

Old chrome version -> reverse engineering time



Reverse engineering

## Part 1.3: Extension to autofill information, cookies and history



## Part 1.4: Extension to different Chromium browsers



Copy and paste

Secure - data authentication



Doing some research, it seemed that extracting data from Windows machines would be the simplest out of the operating systems, utilising API calls to decrypt the data. However, it was more





Extracting the data took significantly longer than anticipated, <-- actually just decrypting



AES MODE, DPAPI

## Reverse engineering the Chromium Source Code



 

Tags: reverse engineering, os, data authentication (DPAPI)

## Data Extraction



Multiple browsers - different encryption schemes, data storage

Tags: sql, decryption

# Part 2: Sending the Data to a Remote Server



#



Hybrid end to end encryption



Tags: networking, encryption, socket programming, malware

# Conclusion

Windows executable for those without Python installed

Environment variables for socket channels?

Apply many concepts learned from course

# Demo and Testing

Designed



Main - just client (no socket)

Remote - server and client





















