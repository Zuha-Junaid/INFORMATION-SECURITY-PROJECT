Project: Academic Portal Security Assessment

Executive Summary

The primary objective of this project was to identify and mitigate security vulnerabilities within a custom-built academic portal. By implementing a defense-in-depth strategy, the assessment utilized multiple security testing methodologies to ensure a robust security posture. The evaluation revealed moderate security risks, primarily involving server misconfigurations and missing security headers.


Methodology & Tools

The assessment employed a hybrid approach, combining automated and manual testing techniques for comprehensive coverage.

Security Testing Framework

Tool/Method  Description

SAST	Static Analysis Security Testing; analyzes source code for hardcoded secrets or unsafe APIs without execution.

DAST	Dynamic Analysis Security Testing; tests the running application for runtime flaws like SQL injection.

IAST	Interactive Analysis; uses agents to monitor real-time application behavior during execution.

SCA	Software Composition Analysis; identifies vulnerabilities in third-party and open-source libraries.

ZAP/Burp Proxy	Intercepts and modifies HTTP traffic to test input validation and session security.

MACRO Tool	Automates complex sequences, such as maintaining authentication during scans

Vulnerability Findings

The scanning process, conducted via OWASP ZAP, identified several critical configuration flaws:


Missing Referrer-Policy: The application fails to instruct the browser on how much referrer information to share, risking the leak of sensitive URLs.


Missing Content-Security-Policy (CSP): The absence of a CSP increases vulnerability to Cross-Site Scripting (XSS) and clickjacking attacks.



Server Banner Disclosure: The server explicitly reveals software versions (e.g., Werkzeug/3.1.5, Python/3.14.2), which assists attackers in targeting version-specific exploits.


Evidence of Scanning

The project utilized automated Macro Event Lists to handle authentication, allowing the DAST tool to access protected areas like the Admin dashboard.

Technical Analysis

Target URL: http://127.0.0.1:8000/ 



Scan Results: The OWASP Penetration Testing Kit (PTK) report identified 2 low-risk findings and 0 critical or high-risk findings.


Captured Headers: Analysis showed the server responding with HTTP/1.1 200 OK but lacking modern security headers.


Pros and Cons of Approach

Pros

Comprehensive Coverage: Using both SAST and DAST ensures code-level and configuration-level flaws are identified.


High Accuracy: IAST integration reduces false positives by correlating runtime data with code analysis.


Cost-Effective: Utilized open-source tools (OWASP) to provide enterprise-grade security without licensing fees.

Cons

Slow Scan Times: DAST scans can be time-consuming for larger applications.


Complexity: Managing and deduplicating results from multiple tools requires significant expertise.

Recommendations & Next Steps

Implement Security Headers: Configure the server to include Content-Security-Policy and Referrer-Policy.


Harden Server: Disable server banners to prevent version fingerprinting.


Continuous Scanning: Integrate SCA into the CI/CD build process to catch vulnerable dependencies early.
