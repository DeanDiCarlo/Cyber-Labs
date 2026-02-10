# Cross-Site Scripting (XSS) – PortSwigger Web Security Academy Labs

## Overview

This lab series focused on identifying and exploiting Cross-Site Scripting (XSS) vulnerabilities using the PortSwigger Web Security Academy platform. The objective was to understand how user-controlled input can be interpreted as executable code by the browser when output handling is improperly implemented.

The lab covered Reflected XSS, Stored XSS, and DOM-based XSS, emphasizing browser execution context, data flow, and client-side trust boundaries.


## Learning Objectives

- Identify XSS vulnerabilities across server-side and client-side contexts
- Distinguish between Reflected, Stored, and DOM-based XSS execution paths
- Analyze how browser parsing and DOM manipulation lead to script execution
- Reinforce defensive techniques used to prevent XSS vulnerabilities


## Environment and Tooling

- PortSwigger Web Security Academy labs
- Burp Suite Chromium
- Browser Developer Tools (DOM inspection, JavaScript analysis)
- Intercepting proxy for request and response inspection

All testing was conducted in an isolated, intentionally vulnerable environment.


## Attack Scenarios and Analysis

### Reflected XSS

**Scenario**  
User input supplied via HTTP request parameters was reflected directly into the HTML response without encoding.

**Analysis**  
Inspection of the server response showed untrusted input being embedded into an HTML context. When rendered by the browser, the injected content was interpreted as executable markup rather than plain text.

**Key Insight**  
Reflected XSS relies on immediate server-side reflection and requires victim interaction, such as visiting a crafted URL.


### Stored XSS

**Scenario**  
User-supplied input submitted through a comment feature was stored persistently and rendered to all subsequent visitors.

**Analysis**  
DOM inspection confirmed that stored content was injected directly into the page without sanitization. The payload executed whenever the affected page was loaded, regardless of user interaction beyond viewing the content.

**Key Insight**  
Stored XSS presents higher risk due to persistence and potential execution in privileged user sessions.


### DOM-Based XSS

**Scenario**  
Client-side JavaScript processed user-controlled data from the browser environment and dynamically inserted it into the DOM.

**Analysis**  
The server response itself contained no malicious content. Instead, JavaScript logic used unsafe DOM manipulation methods, causing browser-side execution when the DOM was updated.

**Key Insight**  
DOM-based XSS occurs entirely on the client side and is often missed by traditional server-side input validation.


## Impact Assessment

Successful exploitation across these scenarios demonstrated that XSS vulnerabilities can enable attackers to:

- Execute arbitrary JavaScript in a trusted origin
- Access session data and browser storage
- Perform authenticated actions as the victim user
- Modify page content for phishing or data exfiltration

The severity of impact depends on the privileges of the affected user and the application’s trust model.


## Defensive Considerations

Mitigation strategies highlighted by these labs include:

- Context-aware output encoding
- Avoidance of unsafe DOM manipulation methods
- Use of secure templating frameworks
- Implementation of Content Security Policy (CSP)
- Limiting inline script execution

Input filtering alone is insufficient to prevent XSS.


## Key Takeaways

- XSS is a client-side vulnerability that abuses browser trust
- Different XSS classes are defined by data flow, not attacker capability
- DOM-based XSS can exist without any server-side reflection
- Proper output handling is the most effective defense

