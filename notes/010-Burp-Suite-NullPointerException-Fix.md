Title: Burp Suite - NullPointerException Fix (Damaged .BurpSuite Profile)

Date: 2026-10-02

Issue
-----
Burp Suite on Kali Linux launched and immediately exited.

Error
-----
Running:

burpsuite

Produced:

[warning] /usr/bin/burpsuite: No JAVA_CMD set for run_java, falling back to JAVA_CMD = java
Could not start Burp: java.lang.NullPointerException: Cannot invoke "burp.Zcie.ZA()" because the return value of "burp.Zdnd.Zw()" is null

Investigation
-------------
Verified Burp installation:

which burpsuite

Output:

/usr/bin/burpsuite

Checked for Burp-related files:

find ~ -iname "*burp*" 2>/dev/null

Output:

/home/kali/.BurpSuite
/home/kali/.BurpSuite/burpbrowser
/home/kali/.java/.userPrefs/burp

Cause
-----
Likely corrupted Burp user profile located in:

~/.BurpSuite

Fix
---
Backup existing profile:

mv ~/.BurpSuite ~/.BurpSuite.bak

Launch Burp again:

burpsuite

Result
------
Burp Suite started successfully.

Notes
-----
- Java was present and Burp was installed.
- Problem was not caused by a missing package.
- Problem was resolved by resetting the user profile.
- Burp automatically generated a new ~/.BurpSuite directory after launch.

Useful Commands
---------------

which burpsuite

find ~ -iname "*burp*" 2>/dev/null

mv ~/.BurpSuite ~/.BurpSuite.bak

burpsuite
