# Google-Bug-Report-Broken-Access-Control
A comprehensive report on a Broken Access Control vulnerability in Google Photos, exposing unauthorized access to private photos. This repository includes proof of concept, impact analysis, and mitigation recommendations for better security practices.

# Summary
Google Photos has a broken access control vulnerability that may expose private user photos to unauthorized access. Insufficient access control checks on media resources allow attackers to view and download media URLs without requiring authentication, which presents a privacy and data confidentiality risk.

# Vulnerability Type
Permissions Bypass

# Affected URL
https://photos.google.com

# Details
Due to insufficient access controls, Google Photos fails to verify authorization when serving media resources. An attacker with network access (e.g., through a shared network or Man-in-the-Middle (MITM) attack) can intercept media URLs and retrieve private photos without authentication.

# OWASP Risk Ranking

This vulnerability aligns with Broken Access Control (A01:2021) in the OWASP Top 10, one of the most severe security flaws due to risks to data confidentiality. This issue is categorized as High under OWASP guidelines because it could expose sensitive, private data without proper authorization.

# Proof of Concept (PoC) Exploitation Steps

    Set Up Burp Suite to Intercept Traffic

    Configure Burp Suite as a proxy to capture HTTP/HTTPS traffic. If possible, install Burp’s certificate in the victim’s browser or intercept on the local network.

2. Capture and Monitor Requests

    The attacker intercepts requests made by a victim user while they view private photos in Google Photos.

3. Identify Vulnerability

    Observe that URLs fetching photos are predictable and do not validate access permissions, e.g., https://lh3.googleusercontent.com/....

4. Access Private Photos

    Paste the captured URL into an incognito browser window to confirm unauthorized access to the media.

# Impact

This vulnerability could enable unauthorized users to view and download private photos without consent. Potential consequences include:

    Data Privacy Violation: Unauthorized access to sensitive media, leading to privacy breaches.
    Exploitation Potential: This predictable URL pattern could allow an attacker to access private photos at scale, violating privacy expectations.

# Attack Scenario

An attacker on the same network (e.g., public Wi-Fi) or conducting a MITM attack could exploit this by intercepting and accessing private URLs.
Mitigations

To protect against unauthorized access:

    Object Ownership Validation: Verify each request for access to media resources to confirm user authorization.
    Session-Based Access Control: Enforce access control by requiring authenticated sessions for each media request to prevent unauthorized direct URL access.


If you’d like to learn more or discuss security research, please feel free to reach out at abhinavsingwal@gmail.com 📧

Feeling generous? You can support my work through a coffee donation ☕: https://buymeacoffee.com/abhinavsingwal

# Disclosure Details

Date — 20-Nov-2024

I am disclosing the details of this vulnerability as per the permissions granted by Google’s bug hunting program. This disclosure is made responsibly, with careful consideration for user security and privacy.

They closed the report and stated that the attack is only possible if the attacker uses MITM techniques. They do not acknowledge any issue with the web application’s access mechanism.
