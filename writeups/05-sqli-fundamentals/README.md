SQL Injection (SQLi) Investigation

PortSwigger Web Security Academy

Overview

This write-up documents a focused investigation into SQL Injection vulnerabilities using PortSwigger Web Security Academy labs and Burp Suite. The work emphasizes understanding SQL execution context, database-specific behavior, and real-world exploitation constraints such as CSRF protection, session handling, and blind inference.

The objective was not just to complete labs, but to understand why each exploit worked, where it failed, and how those lessons translate into defensive security awareness.

Key Accomplishments

Successfully bypassed authentication using SQL injection and identified CSRF and session coupling as real-world blockers to replay attacks

Extracted database version information using Oracle-specific UNION injection techniques

Retrieved administrator credentials from a vulnerable users table while handling column type and rendering constraints

Confirmed and exploited blind SQL injection using time-based delays via cookie injection

Developed strong Burp Suite workflows for SQLi testing using Proxy and Repeater with controlled timing analysis

Lab Summaries
SQL Injection: Authentication Bypass

Primary challenge:
Understanding how to break out of a quoted SQL string while avoiding application-level protections.

Issues encountered:

Initial confusion around string termination and SQL comments

Replay failures caused by CSRF tokens bound to active sessions

Final solution concept:
The injection worked by closing the username string, injecting always-true logic, and commenting out the remainder of the query. Successful exploitation required pairing the injection with a valid CSRF token for the active session.

SQL Injection: Querying Database Version (Oracle)

Primary challenge:
Adapting UNION-based SQL injection to Oracle-specific syntax and output behavior.

Issues encountered:

Repeated 500 errors due to minor syntax mistakes

Output not appearing until the correct reflected column was identified

Final solution concept:
The attack involved determining column count with ORDER BY, using FROM dual for constant selection, and extracting version data from v$version.banner by placing it in the reflected column.

SQL Injection UNION Attack: Credential Extraction

Primary challenge:
Extracting sensitive data when only one column was visibly rendered and another required numeric values.

Issues encountered:

Data type mismatches causing server errors

UNION results appearing in unexpected HTML elements

Final solution concept:
A numeric constant was used for the required numeric column, while credentials were concatenated into the visible string column using SQL string concatenation. Results were filtered to the administrator account to reduce noise and clearly demonstrate impact.

Blind SQL Injection: Time-Based Delay

Primary challenge:
Confirming SQL execution without visible output or error messages.

Issues encountered:

Testing endpoints that did not include the vulnerable cookie

Misleading response timing due to HTTP/2 multiplexing

Encoding differences between URL parameters and cookies

Final solution concept:
The injection was performed through the TrackingId cookie on the correct endpoint using HTTP/1.1. SQL execution was confirmed by reliably triggering a measurable time delay, proving blind SQL injection capability and enabling conditional inference.

Tools and Techniques

Burp Suite Proxy for request discovery and parameter identification

Burp Repeater for controlled payload testing and timing analysis

SQL context analysis including string expressions, UNION compatibility, and database-specific behavior

Careful handling of cookies, encoding, and session state

Security Takeaways

SQL injection defenses must rely on parameterized queries, not input filtering

Blind SQL injection remains highly impactful even when errors and output are suppressed

CSRF protections and session binding can limit exploitability but do not replace secure query construction

Timing anomalies are a strong detection signal for blind SQL injection attempts
