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

   ![Alt Text](https://private-user-images.githubusercontent.com/69685878/388443585-a77f524b-fc41-4fcf-85be-63d580ac3c8e.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzIxODE4NzcsIm5iZiI6MTczMjE4MTU3NywicGF0aCI6Ii82OTY4NTg3OC8zODg0NDM1ODUtYTc3ZjUyNGItZmM0MS00ZmNmLTg1YmUtNjNkNTgwYWMzYzhlLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTIxVDA5MzI1N1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWNkOGM2YmRhZDliN2Y2MDkyOGJiYzNjYmFlY2EzMjZmNmM5MDVjNWEzMzIyNDYwMGM3Yzg4YjQ2NTExN2U4YmUmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.kc1xE7menul4OYDAfMAYYSJIqzS5qSJUveyTzVPFhmA)


5. Access Private Photos

    Paste the captured URL into an incognito browser window to confirm unauthorized access to the media.

   ![Alt Text](https://private-user-images.githubusercontent.com/69685878/388443776-d6071197-b67d-431a-aeb5-ced30db53935.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzIxODE4NzcsIm5iZiI6MTczMjE4MTU3NywicGF0aCI6Ii82OTY4NTg3OC8zODg0NDM3NzYtZDYwNzExOTctYjY3ZC00MzFhLWFlYjUtY2VkMzBkYjUzOTM1LmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTIxVDA5MzI1N1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWM5NGY4MzY1YjkxZDQ5MzJlNTFmMWU1YzMyNDUyZTFmN2I3N2IwZWU3MGJkOGQyYTZkMTU1ZjgwMjFhYmNiMDYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.hZDgJvQZFjKU04EXT9j8M038clmLsUOvTI2KrhSlRyg)


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

![Alt Text](https://private-user-images.githubusercontent.com/69685878/388443763-f8bc2007-1efb-4cac-9c86-34ec1657ce65.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzIxODE4NzcsIm5iZiI6MTczMjE4MTU3NywicGF0aCI6Ii82OTY4NTg3OC8zODg0NDM3NjMtZjhiYzIwMDctMWVmYi00Y2FjLTljODYtMzRlYzE2NTdjZTY1LmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMjElMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTIxVDA5MzI1N1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWU2N2NiMzM4ZjA4MzdhN2RjYjhiNTI3OWJiNjdiM2VlNzI3YmM4YzZmZjIwMjQxZjZmMmMwZDQ4MDRlZTU3YTkmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.jmZc4vD174F0nvVUNq2SuIJGYsfgNJpwYG2eScoBOFY)

