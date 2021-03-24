# Cyber Security Intro

Defender vs attacker mindset

Attackers focus on the weakest points of your defence

Hide jewellry - curtain pole

## Attacker mindset

Thinking like a defender, as counter-intuitive as it may sound, is problematic in security.  It’s easy to get tunnel vision as a defender and overlook areas which are obvious to attackers who have different skills, attitudes and experiences to us. Humans tend to be led into a false sense of security when it comes to reviewing their own work. Have you ever come up with a solution to a problem, only to have significant flaws pointed out after receiving feedback from others? When we only look at a problem from our own perspective, we are bound to overlook areas that others will notice. There’s a simple, but effective adjustment we can make to our way of thinking to improve our defence against attackers. And that’s to think like one.

To truly understand how secure a system is, a defender may hire someone to breach their system. This way vulnerabilities can be identified during pre-deployment. For example a home security company may focus all of their time and effort on a biometric protected access system for the front door and garage of a home. But upon hiring someone to breach the system, the attacker just climbs in through an unlocked window.



# Tuesday

History of cyber

- Microsoft money (online banking)
- Specialisation
- Vulnerability (defect) vs Exploit (getting in)
- Market for 0day's, exploits (pay for services) - market prices indicating security
- Attackers attacking all the time

Mandiant report - 243 median number of days advanced attackers are on the network before being detected

War plane shots example

- Not jumping on first thought
- Looking at bullet shots leading to plane survival rather than non-survival
- Confirmation bias: people often see what they want to see, so as a defender you see the defences made and feel secure. But instead, we need to think about the opposite frame of mind, much like the case with how we only saw the successful planes come back

Data vs Control - when data and control is mixed you are commonly going to get a problem, e.g. telephone calls: playing audio at 2600 Hz would make the call free (an internal-use frequency)

0 Days - vulnerabilities that are not yet noticed by the "good guys" / developers

Black hat vs white hat - motivation shouldn't matter



"The problem of x" - problems to every creation

Security mindset - have to keep looking once you solve a problem, never think you found the perfect solution

Anatomy of an attack: most attacks are going to be a form of social engineering to gain access, then jumping around to find what you need, then leaving. Humans are often the weakest link in the security chain.

Gaining access to secure locations will be a lot more difficult

Reconnaissance: Attackers who first research information about their target and scan for vulnerabilities in their network.

- Active recon: seeking info that can be detected or identified by the target (engaging with the target for info)
- Passive recon: collecting info without engaging with the target

Stages of attack, expansion and obfuscation

Engineering reasonableness check for estimation - \# ants in a room - measuring in smaller chunks rather than volume (gut feeling)

Hallax ship - commision to blame, rather than solve/prevent/response(evacuate)

Single point of failure - a part of a system that, if it fails, will stop the entire system from working

Tamper proof vs tamper evident

# Extension - SQLi

https://youtu.be/bAhvzXfuhg8

```sql
SELECT * FROM sqlite_master WHERE type = 'table'; --- info about all the tables (differ between different sql dbs)

SELECT * FROM table1 WHERE col = '$USER_INPUT'; --- single or double quote
SELECT * FROM table1 WHERE col = '' OR '1' = '1'; --- selects entire table
	$USER_INPUT = ' OR '1' = '1
SELECT * FROM table1 WHERE col = ''; SELECT * FROM table2;-- '; --- allows for query injection
	$USER_INPUT = '; SELECT * FROM table2;-- 
```

==Remember the space after comments *;-- *==

==UNION SELECT queries must have the same number of columns with similar data types==

### [Defence](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html):

- Use of prepared statements (constructed queries)
  - `database.query("SELECT * FROM table1 WHERE col = ?", USER_INPUT)` (modern Python / JS libraries)
- Use of stored procedures (constructed queries inside db)
- Whitelist input validation
- Escaping all user supplied input
- Enforcing least privilege (permissions)

# Tutorial: Case Study 1 - Rumble

Case study: earthquake

- Canopy of tables
- Evacuate to oval

Case study: tsunami

- Rethinking ideas
- Defender mindset - don't give up, keep trying to come up with more ideas

# Week 1 Reflection

Although it's been a busy first week, I thoroughly enjoyed the content learned from attending the lectures and tutorials, as well as from the weekly activities. The lectures opened my eyes to the many different forms of security, especially the connection between physical security and the cyber world. The difference between attacker and defender mindsets and how attackers find the weakest part of the defence is very interesting, for example a burglar breaking into a house despite an 'unbreakable' front door. Now I know that even when designing strong defences, an attacker mindset has to also be considered. I was surprised by my similarities to the "security mindset", including from the reasonableness estimation exercises and my attacker mindset (resiliance and strategies), and I can't wait to see how it develops further. Examing the case studies of earthquake and tsunami survival during our tutorial reinforced the aspect of a defender mindset where although there may not be a perfect solution, better ideas can be generated through not giving up and trying to come up with more ideas as a team. 

Analysing the Wargames movie raised several security issues I had not really thought about before, emphasising the importance of security design, and how there are tradeoffs to every design. I was surprised by how vulnerable systems really are, and how attackers can still break into a system despite one very secure defence measure, learning some of the many different methods of attack through the activities. Having participated in a few CTF's before, I enjoyed working through the cybersecurity activities, especially the practical extension ones involving Steganography and SQL injections. I also found the opportunity for self-learning very helpful and effective personally. Honestly, I spent too much time this week on security, travelling to university for security classes from Monday to Wednesday, then spending the rest of the week completing the many activities. Without a clear indication of how much of the activities were expected to be complete, I managed to complete most of them, mostly because I enjoyed working on the exercises. For the future, I am planning on completing less of the activities as they are really interfering with my workload (four uni subjects this term, two director roles, two peer mentor roles, a part-time job as a software engineer) and focusing more on the ones I find interesting. This would involve starting from the end of the activities with the extension section which were challenges I really enjoyed completing, then selecting some of the activities from each other section that I find interesting and beneficial to my cyber security development as well. 



