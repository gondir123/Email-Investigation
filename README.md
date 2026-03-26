# Email-Investigation

## Objective

To perform a forensic triage of a reported suspicious email, identify Indicators of Compromise (IOCs), and verify the authenticity of the sender to determine if the message poses a threat to the organization.


## Skills Learned

- Email Header Analysis

- Authentication Verification

- Defanging IOCs
  
- De-obfuscation & Decoding

- Using CyberChef for data manipulation

- Identifying Security "Black Boxes

- WHOIS Lookup for IP Address Investigation



## Tools Used

- **Mozilla Thunderbird**: For viewing and managing the suspicious emails.

- **CyberChef**: To defang IP addresses and analyze suspicious strings.

- **MXToolbox**: Employed to verify SPF records, confirming the sending server lacked authorization for the claimed domain.

- **DomainTools**: For performing WHOIS lookups to identify the owner of suspicious IPs.

- **VirusTotal**: To scan and identify malware associated with suspicious email attachments.



## Steps



### 1. Analyze Email Headers

- **Objective**: Extract information about the email's origin and path.

- **Tools Used**: Mozilla Thunderbird, kali linux

- **Action**: Opened sample-1006.eml using Mozilla Thunderbird and inspected the raw "Message Source" to trace the Received hops.

- **Outcome**: Identified the true originating IP address as 109.202.24.52 and noted a geographic mismatch between the sender's claim and the Russian server location.


![Email Header Analysis](https://github.com/gondir123/Email-Investigation/blob/main/Evidence/Screenshot_2026-03-25_01_23_46.png)



### 2. De-obfuscate & Decode Content

- **Objective**: Convert encoded data into human-readable text to identify the hidden threat.
  
- **Tools Used**: CyberChef.
  
- **Action**: Identified that the email body utilized `Content-Transfer-Encoding: quoted-printable`. Extracted the raw body and applied the **"From Quoted Printable"** recipe in CyberChef.
  
- **Outcome**: Successfully revealed the full "Diplomatic Agent" scam script, which claimed a $10.5M USD consignment was waiting at the airport, intended to bait the victim into providing personal address and phone details.

![CyberChef Decoding Process](https://github.com/gondir123/Email-Investigation/blob/main/Evidence/Screenshot_2026-03-25_15_39_51.png)


### 3. Defang & Investigate IOCs

- **Objective**: Safely document Indicators of Compromise (IOCs) and research their global reputation.
  
- **Tools Used**: CyberChef, VirusTotal.
  
- **Action**: Utilized CyberChef to defang `109.202.24.52` and cross-referenced it against threat intelligence databases.
  
- **Outcome**: Confirmed the IP has a "Poor" reputation and is flagged by multiple security vendors for unauthorized spam activity.

![CYBERCHEF Lookup](https://github.com/gondir123/Email-Investigation/blob/main/Evidence/Screenshot_2026-03-26_14_16_00.png)

![CYBERCHEF Lookup](https://github.com/gondir123/Email-Investigation/blob/main/Evidence/Screenshot_2026-03-26_14_33_00.png)

![Virus Total Lookup](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-26_15_05_07.png)



### 4. Verify Authentication & Infrastructure

- **Objective**: Validate the sender's authority and identify the infrastructure owner.
  
- **Tools Used**: MXToolbox, Kali Terminal (WHOIS).
  
- **Action**: Performed an SPF record check on `postfiji.com.fj` and a WHOIS lookup on the originating IP `109.202.24.52`.
  
- **Outcome**: Confirmed an **SPF FAIL**, proving the IP was not authorized. Traced the server to a Russian network (`rosreestr.ru`), contradicting the sender's claim of being a Fiji-based agent.

![MXTOOLBOX Analysis](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-26_15_17_19.png)

![WHOIS LOOKUP](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-26_15_47_00.png)


### 5. Evaluate Security Triage Scores

- **Objective**: Analyze automated security metadata to confirm manual forensic findings.
  
- **Tools Used**: Microsoft Exchange Header Analysis.
  
- **Action**: Inspected the SCL and BCL values to determine how the organization's mail gateway categorized the threat.

- **Outcome**: 
    - **SCL 5**: Confirmed the system identified the message as "Likely Spam."
    - **BCL 9**: Confirmed the originating Russian IP has a history of high-volume bulk/scam distribution.
    - **Final Triage**: Classified as a **Malicious Phishing Attempt (Financial Fraud)**.

![Security Triage Metadata](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-26_15_50_45.png)

 

## Summary of Findings

- **sample-1006.eml**: Phishing attempt posing as a "Diplomatic Agent" from Post Fiji, originating from the Russian IP 109[.]202[.]24[.]52.

-  **X-Sender-IP**: Authenticated as an SPF FAIL, confirming the domain was spoofed to bypass trust filters.
-  
- **Message Body**: De-obfuscated content revealed an Advance Fee Fraud (419 scam) aiming to harvest PII (Personal Identifiable Information).

This investigation showcases the importance of thorough email analysis in identifying potential threats and protecting the organization's security posture. By following structured analysis steps and leveraging various tools like CyberChef, WHOIS, and MXToolbox, it was possible to uncover the malicious intent behind this email and respond accordingly.
