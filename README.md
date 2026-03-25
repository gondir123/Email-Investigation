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





![Email Header Analysis](https://user-images.githubusercontent.com/12345678/123456789-email-header-analysis.png)


![Email Header Analysis](https://github.com/user-attachments/assets/c6c2f574-4d68-4f7d-96b0-5b5772a0fb90)

### 2. Defang IP Addresses


- **Objective**: Make the IP addresses safe to share and analyze.

- **Tools Used**: CyberChef.

- **Action**: Used CyberChef to defang the IP address `204.93.183.11` from the email headers.

- **Outcome**: IP address was successfully defanged for further analysis.




![CyberChef Defanging](https://user-images.githubusercontent.com/12345678/123456789-cyberchef-defang.png)


![CyberChef Defanging](https://github.com/user-attachments/assets/8d68b3b3-d341-409b-9d8c-edf41ebce1f1)



### 3. Perform IP Address Lookup

- **Objective**: Identify the owner of the IP address and gather more details.

- **Tools Used**: Cisco Talos Intelligence, DomainTools.

- **Action**: Looked up the IP address `204.93.183.11` using Cisco Talos Intelligence and DomainTools WHOIS Lookup.

- **Outcome**: Determined that the IP address belonged to `scnet.net`, associated with `Complete Web Reviews`.




![Cisco Talos Lookup](https://user-images.githubusercontent.com/12345678/123456789-cisco-talos.png)


![DomainTools WHOIS Lookup](https://user-images.githubusercontent.com/12345678/123456789-domaintools-whois.png)


![Cisco Talos Lookup](https://github.com/user-attachments/assets/e4d0b246-13c2-461f-a842-4a24b59bc235)


![DomainTools WHOIS Lookup](https://github.com/user-attachments/assets/ead5ed12-706e-4b8f-91ac-587c7af154ac)






### 4. Analyze Suspicious Attachments

- **Objective**: Identify and understand the nature of attachments associated with the suspicious emails.

- **Tools Used**: Mozilla Thunderbird, VirusTotal.

- **Action**: Downloaded and analyzed the attachments from `Email3.eml`, specifically `Sales_Receipt 5606.xls`, using VirusTotal.

- **Outcome**: Identified the malware associated with the attachment as **Dridex**.




![VirusTotal Analysis](https://user-images.githubusercontent.com/12345678/123456789-virustotal.png)


![VirusTotal Analysis](https://github.com/user-attachments/assets/12339404-e4ae-4df4-a06d-37ccfb538df7)




## Summary of Findings

- **Email1.eml**: Phishing attempt posing as LinkedIn, originating from IP `204.93.183.11`.

- **Email2.eml**: Malicious email containing the malware **HIDDENEXT/Worm.Gen**.

- **Email3.eml**: Attached file `Sales_Receipt 5606.xls` was confirmed to be part of the **Dridex** malware family.



This investigation showcases the importance of thorough email analysis in identifying potential threats and protecting the organization's security posture. By following structured analysis steps and leveraging various tools, it was possible to uncover the malicious intent behind these emails and respond accordingly.


