# Day 04 – Web Proxy Fundamentals with Burp Suite

## Overview

This lab focuses on learning **how to use Burp Suite as an HTTP proxy** to observe, modify, and analyze web traffic. The goal was not automated exploitation, but understanding how user-controlled input flows from the browser to the backend and how request manipulation affects server responses.

The lab was completed using PortSwigger Web Security Academy as an intentionally vulnerable and authorized target.


## Objectives

* Configure a browser to route traffic through Burp Suite
* Intercept and inspect HTTP requests and responses
* Identify user-controlled parameters in requests
* Modify request parameters using Burp Repeater
* Observe how backend behavior changes based on modified input
* Document the full request/response workflow


## Environment & Tools

* **Operating System:** Kali Linux
* **Web Proxy:** Burp Suite Community Edition
* **Browser:** Firefox
* **Target Application:** PortSwigger Web Security Academy (authorized lab)


## Lab Setup

1. Launched Burp Suite and verified the Proxy listener was active on `127.0.0.1:8080`
2. Configured Firefox to use Burp as an HTTP proxy
3. Imported Burp’s CA certificate into Firefox to enable HTTPS interception
4. Confirmed traffic visibility in Burp Proxy → HTTP history


## Request Analysis

While navigating the application, a request to the `/filter` endpoint was observed:

```
GET /filter?category=Accessories HTTP/2
```

Analysis showed:

* The `category` parameter is fully user-controlled
* Changing the parameter altered the products returned by the application
* The parameter was likely being used directly in backend query logic

This made it a strong candidate for controlled request manipulation.


## Request Modification (Repeater)

The intercepted request was sent to **Burp Repeater** to allow controlled experimentation without browser interference.

By modifying only the `category` parameter and resending the request, differences in server responses were observed. One modification caused the application to return additional products that were not visible in the original response, indicating that backend filtering logic had been altered.

Key observations:

* The server processed the modified request normally
* The page rendered correctly (no errors)
* Additional products appeared in the HTML response

This confirmed that the request manipulation directly influenced backend behavior.


## Results

* Successfully intercepted and modified HTTP requests
* Demonstrated how user input affects backend logic
* Observed real server-side response changes
* Verified that Burp Repeater sends actual requests to the server, not simulated ones

The lab was marked as **Solved** by the platform after unreleased products were displayed.


## Artifacts

* `original-request.txt` – baseline HTTP request
* `modified-request.txt` – altered request sent via Repeater


## Key Takeaways

* Burp Suite acts as a man-in-the-middle, not a simulation tool
* HTTP parameters must be understood in the context of backend logic
* Repeater is ideal for manual testing and controlled experimentation
* Effective testing requires changing **logic**, not guessing values


## Next Steps

Future labs will build on this foundation by:

* Exploring SQL injection in depth
* Comparing manual testing with automated tooling 
* Expanding Burp usage into authentication and access control testing

This lab establishes the core Burp Suite skills required for deeper web application security analysis.

More to come! This tool seems to have so many nuiances that I am excited to explore.
