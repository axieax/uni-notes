# Monday Lecture

## Trust

Big social groups -> big brain power for thinking about things like trust

Fundamental cybersecurity issue: how to validate data trustworthiness (even biometric sensors)

Impossibility of communication - only one got the necessary message, but both need to know / confirm - two generals problem - cannot have a protocol which guarantees either side got the message

Risk - invisible

Easier to sell fixing a problem than selling preventing a bad thing (invisible) - 

Type 1 and type 2 errors - what you want vs what you get - very closely related, e.g. COVID testing vs whether you have it; left wing right wing

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

- Could be forgotten, cannot control / detect spread
- Cryptographic Properties:
  - Confidentiality
    - Cipher (for recepient through untrusted medium, secret)
      - Classic: Caesar ROT13
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



