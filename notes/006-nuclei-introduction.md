---
title: nuclei introduction
id: 006
---

Nuclei Notes

Date: 2026-09-25

Overview
--------
Nuclei is a template-based security scanning engine developed by ProjectDiscovery.

Unlike traditional scanners, Nuclei executes checks defined in YAML templates.
A template contains requests, matching logic, metadata, and validation rules.

Installation
------------
Update and install templates:

nuclei -update-templates

Template location:

~/.local/nuclei-templates

Main Template Categories
------------------------
http/
dns/
network/
ssl/
headless/
javascript/
workflows/
dast/

HTTP Categories
---------------
cves
technologies
misconfiguration
fuzzing
exposures
exposed-panels
default-logins
takeovers
vulnerabilities

Exploration Commands
--------------------

List categories:

ls ~/.local/nuclei-templates/http

Find Next.js related templates:

find ~/.local/nuclei-templates/http -maxdepth 2 -type d | grep next

Output:

http/default-logins/next-terminal
http/vulnerabilities/nextjs

List Next.js vulnerability templates:

find ~/.local/nuclei-templates/http/vulnerabilities/nextjs -type f

Output:

next-js-cache-poisoning.yaml
nextjs-rsc-cache.yaml
nextjs-middleware-cache.yaml

Template Analysis
-----------------
Reviewed:

nextjs-middleware-cache.yaml

Purpose:
Detect potential cache poisoning behavior in Next.js applications.

Technique:
1. Send requests with the header:

   X-Middleware-Prefetch: 1

2. Observe response headers.

3. Check for:

   X-Middleware-Skip: 1

4. Verify response caching behavior through Cache-Control and Pragma headers.

Key Observation
---------------
Nuclei templates are effectively automated Proof-of-Concept checks.

A template usually consists of:

- one or more HTTP requests
- response matchers
- logical conditions
- metadata
- 
