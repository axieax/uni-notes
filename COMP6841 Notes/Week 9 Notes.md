



# Extension: Malware Analysis

- Types of malware
  - Adware
  - Bot
  - Ransomware (evolving to doxware - blackmail)
  - Rootkits
  - Spyware
  - Virus
  - Worm
  - Trojan
- Methodology
  - Do no harm - no permanent damage to your computer, other's computers - VM (with snapshots), only connected to what's necessary
  - Need to know - system to system communication (data in and out - am I being compromised in analysing it - let communication happen or prevent?)
  - Discover, document, review - write down findings and look for other things that support that conclusion
- Purpose
  - Improve defence
  - Config (variant)
  - Targeting (find target)
  - CnC (command and control - blacklist IP address - cut communication, IP to law enforcement)
  - Vulnerabilities (malware as well as other software / Microsoft OS)
  - Attribution (could be faked to look like it was from someone else)
- Static analysis
  - Not executing anything
  - Often enough to recover domain names, CnC IP addresses, config data
  - Signaturing - regex on binary data - similar files may have similar config data, IP addresses, delay times, file paths
  - Slow and complicated
  - IDA - .exe PE format
- Dynamic analysis
  - Controlled environment (VM, even though there are VM escapes/vulnerabilities) - monitoring free behaviour or breakpoints after each instruction (debugger)
  - Monitor external internet communications (TCP/IP, DNS traffic), file changes
  - Can be performed at scale (automated analysis)
  - Patching - replace instruction with another one
  - Dangers
    - Harm - VM escapes/vulnerabilities
    - Allowing communication - may send encrypted stuff (don't know what of) - e.g. could be saying that you are analysing the malware with IP/MAC address to identify you - may attack you specifically or use a different variant of the malware instead
  - Fakenet program
- Static analysis notes
  - Libraries can also be loaded in dynamically and missed by static analysis, also encryption keys can be fetched from server
  - Hardcoded static IP addresses, domain names, file paths/names
  - Breakdown of areas in memory - unexplored or gap (headers) - IDA can't find anything there - malware might modify itself (e.g. unpack part of itself into one of these sections, decrypt, modify itself)
  - VirusTotal - requires uploading (may not be allowed, will be executed - telling authors of malware that you're analysing it) - can use file hash
    - Detection - runs in virtual environments against antivirus programs
    - Details - header info, hashes, other names, creation time
    - Relations - domain names and ip addresses contacted - may be false positives
    - Behaviour - automated dynamic analysis in a sandbox environment - may tell malware author that you're analysing it
- Dynamic analysis notes
  - fakenet monitors traffic and saves as pcap (package capture) file, which can be analysed in Wireshark
  - Procmon (Windows) monitors file changes, which can be analysed with procdot (csv file) - graph view
    - Files may store data about malware and how it runs
    - Malware install to a location and check if it's already been installed there
    - May edit registry - key/value pairs for OS - persistence, modifying how OS runs etc.
    - Changed user files
  - Debugger (x32dbg Windows) - exactly what program is doing - not anti-analysis
    - Can step over function calls to dll
    - Program can run on multiple threads at the same time
    - Modify instructions
- Anti-analysis
  - Obfuscation (unnecessary instructions, packers - anti static analysis)
  - Virtualisation (can figure out if environment is virtual - remote server response, \#files on machine, \#files recently opened in Microsoft Excel for example)
  - Debugger detection (isDebuggerPresent)
  - Exploit analysis - e.g. targeting IDA analysis which makes assumptions based on stack frames, tricking user analysing - try to break out of specific virtual machines (such as VirtualBox) and infect the host machine

