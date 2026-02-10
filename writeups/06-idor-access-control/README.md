# Access Control & IDOR Vulnerabilities  
**PortSwigger Web Security Academy**

## Overview
This lab series focuses on identifying and exploiting **broken access control vulnerabilities**, including **privilege escalation** and **Insecure Direct Object References (IDOR)**. The emphasis is on understanding how authorization failures occur independently of authentication and how business logic assumptions lead to critical security flaws.

All work was performed in intentionally vulnerable training environments.


## Skills Practiced
- Access control analysis (vertical, horizontal, context-dependent)
- Identifying missing or inconsistent authorization checks
- Exploiting IDOR via parameter manipulation
- Privilege escalation through workflow abuse
- Manual request crafting and replay
- Session cookie handling and context switching
- Mapping application logic to security impact


## Key Concepts
- **Authentication** verifies identity
- **Session management** tracks user requests
- **Authorization** determines allowed actions

Broken access control occurs when authorization is:
- Missing
- Client-controlled
- Applied inconsistently
- Assumed rather than enforced


## Vulnerability Types Explored

### Vertical Privilege Escalation
- Unprotected admin endpoints
- Hidden or obfuscated admin URLs
- Role or privilege controlled by request parameters or cookies

### Horizontal Privilege Escalation (IDOR)
- User identifiers controlled by request parameters
- Accessing other users’ data by modifying IDs or usernames
- Exploiting leaked or guessable identifiers

### Horizontal → Vertical Escalation
- Using horizontal access to compromise privileged accounts
- Gaining administrative functionality via another user’s workflow


## Notable Exploits Completed
- Unprotected admin functionality
- Unpredictable admin URL exposure
- Role modification via request parameters
- IDOR with predictable and unpredictable identifiers
- Multi-step process missing access control
- Insecure direct object references


## Key Challenge
One advanced lab required abusing a **multi-step privilege upgrade process**:

- Captured and saved the final-stage HTTP request
- Logged into a separate account
- Replaced the session cookie in the saved request
- Modified the target username parameter
- Replayed the request out of sequence

The application failed to re-check authorization at the final step, resulting in unauthorized privilege escalation.


## Tools Used
- Burp Suite (Proxy, Repeater)
- Manual HTTP request analysis
- Browser developer tools


## Security Takeaways
- Authorization must be enforced **server-side**
- Every sensitive action requires its own access check
- Never trust:
  - Client-side parameters
  - Cookies indicating roles
  - Workflow order assumptions
- Obfuscation is not access control
- Deny-by-default should be the standard


## Ethics & Scope
All testing was conducted exclusively in authorized PortSwigger training labs.  
No real-world systems were tested.
