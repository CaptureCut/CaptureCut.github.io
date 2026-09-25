---
title: FFUF
id: 004
---

# 004-ffuf

## Overview

FFUF (Fuzz Faster U Fool) is a fast web fuzzing tool used for content discovery and enumeration.

Common use cases:

- Directory discovery
- File discovery
- Virtual host discovery
- Parameter fuzzing
- Endpoint enumeration

Repository:
https://github.com/ffuf/ffuf

---

## Basic Syntax

Target path contains the keyword FUZZ.

Example:

ffuf -u http://target/FUZZ -w wordlist.txt

FFUF replaces FUZZ with entries from the supplied wordlist.

---

## Important Options

-u
Target URL.

-w
Wordlist.

-mc
Match status codes.

Example:

ffuf -u http://target/FUZZ \
-w wordlist.txt \
-mc 200,301,302

-fc
Filter status codes.

Example:

ffuf -u http://target/FUZZ \
-w wordlist.txt \
-fc 404

-fs
Filter responses by size.

Example:

ffuf -u http://target/FUZZ \
-w wordlist.txt \
-fs 1234

-e
File extensions.

Example:

ffuf -u http://target/FUZZ \
-w wordlist.txt \
-e .php,.txt,.html

-recursion
Enable recursive scanning.

-v
Verbose output.

---

## Common Status Codes

200
Resource accessible.

301
Redirect.
Often indicates a directory.

302
Temporary redirect.

403
Resource exists but access denied.

404
Not found.

500
Server error.

---

## Basic Directory Enumeration

ffuf -u http://target/FUZZ \
-w /usr/share/wordlists/dirb/common.txt

Results may include:

admin
uploads
backup
config
secret

---

## Extension Discovery

ffuf -u http://target/FUZZ \
-w wordlist.txt \
-e .php,.txt,.bak

Possible findings:

admin.php
backup.bak
config.txt

---

## Virtual Host Fuzzing

ffuf -u http://target \
-H "Host: FUZZ.target.local" \
-w wordlist.txt

Used to discover hidden virtual hosts.

---

## Verification Workflow

Enumeration should not stop after finding a resource.

Process:

Run ffuf
↓
Review results
↓
Verify manually
↓
Explore deeper
↓
Document findings

Example:

ffuf finds:

.ssh [301]

Verify:

curl http://127.0.0.1:8000/.ssh/

Result:

Directory listing enabled.

Continue enumeration inside discovered directories.

---

## Local Practice Lab

Server:

python3 -m http.server 8000

Scan:

ffuf -u http://127.0.0.1:8000/FUZZ \
-w /usr/share/wordlists/dirb/common.txt

Observed findings:

.bashrc
.profile
.ssh
.config
.cache
Downloads
Music
Projects
research

Verification:

curl http://127.0.0.1:8000/.bashrc

Result:

Accessible file content.

Verification:

curl http://127.0.0.1:8000/.ssh/

Result:

Directory listing revealed:

agent/

Further exploration:

curl http://127.0.0.1:8000/.ssh/agent/

Result:

s.RDJpj98jBr.agent.pRu7mJiXWC

---

## Lessons Learned

- FFUF is primarily an enumeration tool.
- Wordlists drive discovery.
- Status codes provide context about findings.
- Findings require manual verification.
- Enumeration is recursive.
- Directory listings can reveal additional content.
- Discovery is only the beginning of investigation.

---

## Personal Notes

Today I practiced FFUF against a local Python HTTP server.

Key observations:

- Successfully discovered exposed files.
- Successfully discovered exposed directories.
- Verified findings using curl.
- Observed directory listing behavior.
- Followed a basic enumeration workflow.
- Practiced moving from discovery
