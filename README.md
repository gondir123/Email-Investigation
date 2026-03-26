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



![Email Header Analysis](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-25_01_23_46.png)



### 2. De-obfuscate & Decode Content

- **Objective**: Convert encoded data into human-readable text to identify the hidden threat.
  
- **Tools Used**: CyberChef.
  
- **Action**: Identified that the email body utilized `Content-Transfer-Encoding: quoted-printable`. Extracted the raw body and applied the **"From Quoted Printable"** recipe in CyberChef.
  
- **Outcome**: Successfully revealed the full "Diplomatic Agent" scam script, which claimed a $10.5M USD consignment was waiting at the airport, intended to bait the victim into providing personal address and phone details.

![CyberChef Decoding Process](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-25_15_39_51.png)


### 3. Defang & Investigate IOCs

- **Objective**: Safely document Indicators of Compromise (IOCs) and research their global reputation.
  
- **Tools Used**: CyberChef, VirusTotal.
  
- **Action**: Utilized CyberChef to defang `109.202.24.52` and cross-referenced it against threat intelligence databases.
  
- **Outcome**: Confirmed the IP has a "Poor" reputation and is flagged by multiple security vendors for unauthorized spam activity.

![CYBERCHEF Lookup](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-26_14_16_00.png)

![CYBERCHEF Lookup](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-26_14_33_00.png)

![Virus Total Lookup](https://github.com/gondir123/Email-Investigation/blob/main/Screenshot_2026-03-26_15_05_07.png)



### 4. Verify Authentication & Infrastructure

- **Objective**: Validate the sender's authority and identify the infrastructure owner.
  
- **Tools Used**: MXToolbox, Kali Terminal (WHOIS).
  
- **Action**: Performed an SPF record check on `postfiji.com.fj` and a WHOIS lookup on the originating IP `109.202.24.52`.
  
- **Outcome**: Confirmed an **SPF FAIL**, proving the IP was not authorized. Traced the server to a Russian network (`rosreestr.ru`), contradicting the sender's claim of being a Fiji-based agent.

![WHOIS Infrastructure Trace](YOUR_GITHUB_URL_HERE)




![VirusTotal Analysis](https://user-images.githubusercontent.com/12345678/123456789-virustotal.png)


![VirusTotal Analysis](https://github.com/user-attachments/assets/12339404-e4ae-4df4-a06d-37ccfb538df7)


### 5.  Evaluate Security Triage Scores

- **Objective**: Analyze how automated enterprise filters categorized the threat.

- **Tools Used**: Microsoft Exchange Header Analysis.

- **Action**:Inspected the SCL (Spam Confidence Level) and BCL (Bulk Complaint Level) values within the metadata.
  
- **Outcome**: Verified an SCL of 5, confirming the message was correctly identified as high-risk spam by the organization's security controls.







## Summary of Findings

- **Email1.eml**: Phishing attempt posing as LinkedIn, originating from IP `204.93.183.11`.

- **Email2.eml**: Malicious email containing the malware **HIDDENEXT/Worm.Gen**.

- **Email3.eml**: Attached file `Sales_Receipt 5606.xls` was confirmed to be part of the **Dridex** malware family.



This investigation showcases the importance of thorough email analysis in identifying potential threats and protecting the organization's security posture. By following structured analysis steps and leveraging various tools, it was possible to uncover the malicious intent behind these emails and respond accordingly.


