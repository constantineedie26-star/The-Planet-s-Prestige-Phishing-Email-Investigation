# 📧 The Planet's Prestige: Phishing Email Investigation

<div align="center">

![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![Type](https://img.shields.io/badge/Investigation-Phishing-blue?style=for-the-badge)
![Difficulty](https://img.shields.io/badge/Level-Intermediate-orange?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows%2011-0078D6?style=for-the-badge&logo=windows)
![Focus](https://img.shields.io/badge/Focus-Digital%20Forensics-red?style=for-the-badge)
![SOC](https://img.shields.io/badge/SOC-Incident%20Investigation-darkgreen?style=for-the-badge)

</div>

---

# Executive Summary

## Overview

This project documents a complete phishing email investigation conducted in an isolated Windows 11 virtual machine as part of a hands-on Digital Forensics and Incident Response (DFIR) exercise.

The objective was to determine whether a suspicious email represented malicious activity by examining its headers, validating email authentication, decoding hidden content, verifying attachment integrity, recovering concealed artifacts, and documenting the investigation using industry-standard incident response practices.

Throughout the investigation, multiple Indicators of Compromise (IOCs) were identified, including spoofed sender information, failed SPF authentication, Base64-encoded content, hidden files, and a disguised attachment. The collected evidence was analyzed to reconstruct the attack chain and produce a professional incident report.

This project demonstrates practical skills commonly used by Tier 1 Security Operations Center (SOC) Analysts during phishing investigations, evidence collection, and incident documentation.

---

# Project Overview

Phishing remains one of the most common initial access techniques used by threat actors. Modern phishing campaigns frequently employ deceptive tactics such as spoofed email identities, misleading file extensions, encoded payloads, hidden artifacts, and social engineering to bypass technical controls and manipulate end users.

In this investigation, a suspicious email was analyzed from initial receipt through forensic examination of its attachment. Multiple investigative techniques were applied to validate the authenticity of the email, uncover concealed information, and identify indicators that could support future detection and response efforts.

Rather than focusing solely on identifying malicious artifacts, this project follows the structured investigative methodology used within Security Operations Centers (SOC) to document findings, preserve evidence, and communicate risk effectively.

---

# Scenario

An Army Major reported receiving a suspicious email titled **"A Hope to CoCanDa."**

The sender claimed responsibility for the disappearance of several individuals and demanded a ransom while instructing the recipient to open an attached document.

Initial inspection revealed several suspicious characteristics, prompting a full forensic investigation to determine whether the email was legitimate, identify indicators of compromise, and recover any concealed evidence contained within the attachment.

---

# Investigation Objectives

The primary objectives of this investigation were to:

- Validate the authenticity of the suspicious email.
- Examine email headers to identify sender infrastructure.
- Verify SPF authentication results.
- Decode Base64-encoded content.
- Determine the true file type of the attachment.
- Recover hidden files contained within the archive.
- Analyze document metadata for investigative value.
- Identify Indicators of Compromise (IOCs).
- Document findings using professional incident response methodology.

---

# Skills Demonstrated

- Email Security Investigation
- Phishing Analysis
- Digital Forensics
- Incident Response
- Threat Hunting
- Email Header Analysis
- File Signature Verification
- Base64 Decoding
- Metadata Analysis
- IOC Identification
- Incident Documentation
- Analytical Problem Solving

---

# Tools & Environment

| Category | Tools Used |
|------------|------------------------------|
| Operating System | Windows 11 Virtual Machine |
| Investigation | File Explorer |
| Email Analysis | Email Header Inspection |
| Encoding Analysis | Cyberchef(Base64 Decoder) and HxD Decoder |
| File Validation |Kessler File Signature Analysis |
| Digital Forensics | Metadata Examination |
| Documentation | Markdown |

---

# Investigation Workflow

```text
Suspicious Email

        │
        ▼

Email Header Analysis

        │
        ▼

SPF Authentication Review

        │
        ▼

Base64 Decoding

        │
        ▼

Attachment Validation

        │
        ▼

File Signature Verification

        │
        ▼

Archive Extraction

        │
        ▼

Hidden File Discovery

        │
        ▼

Metadata Analysis

        │
        ▼

IOC Collection

        │
        ▼

Incident Documentation
```

---

---

# 🔬 Technical Investigation

This section documents the investigative process used to analyze the suspicious email, validate its authenticity, recover hidden evidence, and identify Indicators of Compromise (IOCs). Each phase follows a structured methodology similar to the workflow performed by Tier 1 Security Operations Center (SOC) Analysts during phishing investigations.

---

# Phase 1-Email Header Analysis

## Objective

Determine the origin, authenticity, and routing path of the suspicious email by analyzing its header information.

## Investigation

The investigation began with a detailed review of the email headers to identify the sender, recipient, routing infrastructure, authentication results, and message metadata.

Several anomalies were immediately observed, indicating the email required further investigation.

### Key Observations

| Field | Observation |
|---------|-------------|
| Subject | A Hope to CoCanDa |
| Sender | billjobs@microapple.com |
| Reply-To | negeja3921@pashter.com |
| Recipient | themajoronearth@gmail.com |
| Sending Host | emkei.cz |
| Source IP | 93.99.104.210 |
| SPF Authentication | Failed |

### Initial Assessment

The email exhibited several characteristics commonly associated with phishing attacks.

Notable indicators included:

- Sender and Reply-To addresses used different domains.
- Email authentication failed SPF validation.
- Email originated from an unexpected sending host.
- Sender identity could not be fully trusted.

The email failed SPF authentication because the sending IP address 93.99.104.210 was not authorized to send email on behalf of microapple.com.

The visible sender was billjobs@microapple.com, while the Reply-To address was negeja3921@pashter.com. This meant replies would be directed to a different domain.

These findings justified continuing the investigation.

---
# Email Header Analysis:

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/8a922390eb7101ef5eb9b75c07747836dac05f44/Screenshot%202026-08-08%20150712.png)

---

# Phase 2-SPF Authentication Analysis

## Objective

Verify whether the sending server was authorized to send email on behalf of the claimed sender's domain.

## Investigation

Sender Policy Framework (SPF) validation was examined to determine whether the sending infrastructure matched the domain owner's published SPF policy.

### Result

| Authentication | Status |
|----------------|--------|
| SPF | ❌ Failed |

### Analyst Notes

The failed SPF validation indicated that the sending server was not authorized to transmit email using the claimed sender's domain.

Although an SPF failure alone does not confirm malicious activity, it significantly increases suspicion when combined with other phishing indicators.

---

# Spf Analysis:

![SPF](spf%20file.png)

---

# Phase 3-Base64 Decoding

## Objective

Decode encoded content to determine whether hidden information was embedded within the email or attachment.

## Investigation

Analysis revealed that portions of the email body and attachment had been encoded using Base64.

The encoded data was decoded to expose the original content for forensic examination.

### Findings

- Email body contained Base64-encoded data.
- Attachment also contained encoded content.
- Decoded information provided additional evidence for the investigation.

### Analyst Notes
The provided evidence was an `.eml` file named `A Hope to CoCanDa.eml`. I opened the file in Notepad++ to review the raw email contents, including the headers, MIME structure, encoded message body, and attachment information.

The email was identified as a multipart MIME message containing a Base64-encoded plain-text body. After decoding the body in CyberChef, I identified a ransom demand and instructions to solve an attached puzzle.

---

# Base64 Decoding:
The raw email showed a multipart MIME structure and a Base64-encoded plain-text body:

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/39715b976a702cbdbadfcfebd3c0daa8ae239ae0/Base64%20encoded.png)

I copied and pasted the Base64-encoded message body into CyberChef and decoded it using the From Base64 operation.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/d81106c94cf3abe7f8500bd65b82c761fa160e9b/Base64%20decoded.png)

Base64 encoding is commonly used to transport binary data within email messages.

Although Base64 is not encryption, threat actors frequently use it to obscure malicious content from casual inspection.



# Phase 4-Attachment Verification

## Objective

Determine whether the attachment accurately represented its advertised file type.
This mismatch showed that the attachment was presented as a PDF even though its file signature identified it as a ZIP-based archive. Because the file type did not match the declared extension, I continued the analysis inside an isolated Windows virtual machine.

## Investigation

The email contained an attachment named:

```
PuzzleToCoCanDa.pdf
```

Initial appearance suggested the attachment was a PDF document.

However, file signature analysis was performed to verify the file's true identity.


### 📎 Attachment Analysis

| **Attribute** | **Value** |
|:--------------|:----------|
| **Declared Filename** | `PuzzleToCoCanDa.pdf` |
| **Declared Content Type** | `application/pdf` |
| **Transfer Encoding** | `Base64` |
| **Observed File Signature** | `50 4B 03 04` |
| **Identified File Type** | `ZIP Archive` |
| **Finding** | The attachment was disguised as a PDF, but file-signature analysis confirmed it was a ZIP archive, indicating an attempt to conceal its true content. |

The attachment had been intentionally disguised using a misleading file extension.

---
The raw email contained an attachment named PuzzleToCoCanDa.pdf. Its MIME headers declared it as an application/pdf, and its contents were encoded using Base64.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/98ddcb30f7a2b4fe588d6e667a00c70dc57c01ea/Attachment%20file.png)

`Kind Note`: All attachment analysis and file extraction were performed inside an isolated Windows virtual machine.

---

# Phase 5-File Signature Verification

## Objective

Validate the attachment's true file type using its binary file signature (magic number).

## Investigation

Rather than relying on the file extension, the file header was examined.

### Magic Number

```
50 4B 03 04
```

### Result

The signature identified the attachment as a ZIP archive instead of a PDF document.

To validate the attachment's true file type, I analyzed its Base64-encoded content in CyberChef by applying the `From Base64` operation followed by `To Hex`, enabling examination of the file's first four-byte signature.

![Image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/e316a19f2419df8c8af2986f10110f6707184d77/To%20Hex%20Byte.png)

Threat actors frequently disguise malicious files by changing their extensions while leaving the underlying file format unchanged.

File signature analysis is a critical forensic technique for detecting disguised files.

---

# Phase 6-Archive Extraction

## Objective

Safely extract the archive within an isolated environment to identify its contents.

## Investigation

The archive was extracted inside an isolated Windows 11 Virtual Machine to prevent accidental execution on the host system.

Three files were recovered during extraction.

| Recovered File | Identified Type |
|----------------|-----------------|
| DaughtersCrown | JPEG Image |
| GoodJobMajor | PDF Document |
| Money.xlsx | Hidden Spreadsheet |

Having confirmed the attachment's true file type as a ZIP archive, I modified the CyberChef workflow by removing the To Hex operation and exported the decoded content as email_attachment.zip, enabling detailed analysis of the extracted files.

[!image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/a4c6e2a79d00d9158b5dbba519af2598724c2d02/Email%20extraction.png)

The ZIP archive was extracted and examined within an isolated Windows 11 virtual machine, ensuring a controlled environment for safely analyzing its contents while protecting the host system.
![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/a4c6e2a79d00d9158b5dbba519af2598724c2d02/Archive%20extraction.png)

---

<details>

<summary><strong>📸 View Archive Extraction Screenshots</strong></summary>

Insert screenshots showing the extracted archive contents.

</details>

---

# Phase 7-Hidden File Analysis

## Objective

Identify concealed evidence contained within the extracted archive.

## Investigation

One spreadsheet remained hidden during initial inspection.

Further analysis revealed concealed Base64-encoded information embedded within the spreadsheet.

After decoding the hidden content, the following location was recovered:

> **The Martian Colony, Beside Interplanetary Spaceport**

### Analyst Notes

Hidden files and concealed data are common techniques used to delay detection and complicate forensic investigations.

---

<details>

<summary><strong>📸 View Hidden Spreadsheet Screenshots</strong></summary>

Insert screenshots showing the hidden spreadsheet and decoded content.

</details>

---

# Phase 8-Metadata Analysis

## Objective

Examine document metadata for additional forensic artifacts.

## Investigation

Metadata analysis identified the following document author:

```
Pestero Negeja
```

### Assessment

Although metadata can provide useful investigative leads, it should never be considered definitive attribution because document properties can be modified.

Metadata should always be corroborated with additional evidence.

---

<details>

<summary><strong>📸 View Metadata Analysis Screenshots</strong></summary>

Insert screenshots showing metadata analysis.

</details>

---

# Evidence Collected

| Evidence | Description |
|-----------|-------------|
| Email Headers | Sender information and routing path |
| SPF Results | Failed authentication |
| Base64 Content | Decoded email and attachment |
| File Signature | ZIP archive masquerading as PDF |
| Extracted Files | JPEG, PDF, Hidden Spreadsheet |
| Metadata | Document author information |
| Final Location | The Martian Colony, Beside Interplanetary Spaceport |

---

## Phase Summary

Throughout the investigation, multiple Indicators of Compromise were identified by correlating email header analysis, authentication results, file validation, encoded content, hidden artifacts, and document metadata. Each stage contributed valuable evidence that enabled the reconstruction of the attack and prepared the investigation for formal reporting in the next phase.

---

# 📑 Professional Investigation Report

This section consolidates the evidence collected throughout the investigation into a structured incident report. The objective is to clearly communicate the nature of the threat, document the investigative findings, identify Indicators of Compromise (IOCs), and recommend defensive actions. This reporting format aligns with documentation practices commonly used by Security Operations Center (SOC) analysts during phishing investigations.

---

# Executive Findings

The investigation confirmed that the email was a **simulated phishing attack** designed to deceive the recipient through social engineering and multiple evasion techniques.

Analysis identified several Indicators of Compromise (IOCs), including a spoofed sender identity, failed SPF authentication, Base64-encoded content, a disguised ZIP archive presented as a PDF document, hidden files, and manipulated metadata.

No malware execution occurred during the investigation because all analysis was performed inside an isolated Windows 11 virtual machine.

The concealed evidence was successfully recovered, allowing the investigation to reconstruct the attack methodology and identify the hidden location embedded within the spreadsheet.

---

# Incident Summary

| Category | Details |
|-----------|---------|
| Incident Type | Phishing Email Investigation |
| Severity | Medium |
| Status | Closed |
| Investigation Outcome | Completed Successfully |
| Environment | Windows 11 Virtual Machine |
| Evidence Preserved | Yes |

---

# Investigation Findings

| Finding | Description |
|----------|-------------|
| Email Authentication | SPF validation failed. |
| Sender Identity | Sender and Reply-To domains did not match. |
| Email Origin | Message originated from **emkei.cz** (9399.104.210). |
| Attachment | Advertised as a PDF but verified as a ZIP archive. |
| Hidden Content | Base64-encoded data discovered within a hidden spreadsheet. |
| Metadata | Author listed as **Pestero Negeja** (not sufficient for attribution). |
| Final Evidence | Hidden message revealed **The Martian Colony, Beside Interplanetary Spaceport**. |

---

# Who, What, When, Where, Why & How

## Who

The phishing email targeted **themajoronearth@gmail.com** while impersonating the sender **billjobs@microapple[.]com**. A different Reply-To address was used, indicating an attempt to conceal the sender's true identity.

---

## What

A phishing email attempted to persuade the recipient to open a disguised attachment. Further investigation revealed that the attachment contained hidden files and concealed information rather than the advertised PDF document.

---

## When

| Date | Time | Time Zone |
|------|------|-----------|
| January 26, 2021 | 1:41:18 AM | EST |

No evidence indicated additional activity beyond the delivery of the email.

---

## Where

| Evidence | Value |
|----------|-------|
| Recipient | themajoronearth@gmail.com |
| Sending Host | emkei.cz |
| Source IP | 93.99.104.210 |
| Hidden Location | The Martian Colony, Beside Interplanetary Spaceport |

---

## Why

The attacker attempted to manipulate the recipient using a fabricated ransom scenario. Evidence recovered during forensic analysis suggests the message was designed to mislead the recipient while concealing its true objective through multiple layers of obfuscation.

---

## How

The phishing campaign employed several techniques commonly observed in modern email attacks:

- Sender spoofing
- Failed SPF authentication
- Sender and Reply-To mismatch
- Base64 encoding
- File extension masquerading
- Hidden spreadsheet
- Concealed Base64 content
- Document metadata manipulation

---

# Key Indicators of Compromise (IOCs)

## Email Indicators

| IOC Type | Indicator |
|-----------|-----------|
| Subject | A Hope to CoCanDa |
| Sender | billjobs@microapple.com |
| Reply-To | negeja3921@pashter.com |
| Recipient | themajoronearth@gmail.com |

---

## Infrastructure Indicators

| IOC Type | Indicator |
|-----------|-----------|
| Sending Host | emkei.cz |
| Source IP | 93.99.104.210 |

---

## File Indicators

| IOC Type | Indicator |
|-----------|-----------|
| Attachment | PuzzleToCoCanDa.pdf |
| Actual Type | ZIP Archive |
| Hidden File | Money.xlsx |
| Metadata Author | Pestero Negeja |

---

# MITRE ATT&CK Mapping

| Technique ID | Technique | Description |
|--------------|-----------|-------------|
| T1566.001 | Spearphishing Attachment | Delivery of a malicious attachment via email. |
| T1036 | Masquerading | ZIP archive disguised as a PDF document. |
| T1027 | Obfuscated Files or Information | Base64 encoding used to conceal content. |
| T1140 | Deobfuscate/Decode Files | Base64 decoding performed during analysis. |
| T1562 | Impair Defenses | Attempted evasion through spoofed identities and misleading attachments. |

---

# Attack Timeline

| Stage | Activity |
|---------|----------|
| 1 | Phishing email delivered |
| 2 | Email headers analyzed |
| 3 | SPF authentication reviewed |
| 4 | Base64 content decoded |
| 5 | Attachment verified |
| 6 | File signature inspected |
| 7 | ZIP archive extracted |
| 8 | Hidden spreadsheet discovered |
| 9 | Metadata analyzed |
| 10 | Indicators of Compromise documented |
| 11 | Investigation report completed |

---

# Analyst Assessment

This investigation successfully demonstrated the importance of correlating multiple sources of evidence rather than relying on a single indicator.

Although the attachment initially appeared to be a harmless PDF document, forensic analysis revealed layered deception techniques designed to evade casual inspection. By validating email authentication, inspecting file signatures, decoding hidden content, and analyzing document metadata, the investigation successfully reconstructed the attack chain and documented the evidence using structured incident response methodology.

The techniques observed throughout this investigation closely resemble tactics commonly encountered during real-world phishing investigations performed by Tier 1 Security Operations Center (SOC) analysts.

---

### Key Takeaways

- Email headers provide critical evidence during phishing investigations.
- SPF failures should always be investigated in combination with other indicators.
- File extensions alone cannot determine a file's true type.
- File signature analysis is essential when validating suspicious attachments.
- Base64 encoding is frequently used to conceal malicious content.
- Hidden files may contain valuable forensic evidence.
- Document metadata can provide useful investigative leads but should never be considered definitive attribution.
- Correlating multiple indicators produces more reliable investigative conclusions than relying on a single artifact.

---

# 📊 MITRE ATT&CK Coverage

| Tactic | Technique | ID |
|---------|-----------|----|
| Initial Access | Spearphishing Attachment | T1566.001 |
| Defense Evasion | Masquerading | T1036 |
| Defense Evasion | Obfuscated Files or Information | T1027 |
| Defense Evasion | Deobfuscate/Decode Files | T1140 |

---

# 🧠 SOC Analyst Reflection

One of the most valuable lessons from this investigation was understanding that phishing analysis extends far beyond simply identifying suspicious emails.

Each stage of the investigation required collecting evidence, validating assumptions, correlating artifacts, and documenting findings in a structured manner. By following a methodical investigative process, it became possible to uncover hidden indicators, reconstruct the attack chain, and communicate the findings in a professional incident report.

This project reflects the investigative mindset required of Security Operations Center (SOC) analysts and highlights the importance of attention to detail, analytical thinking, and evidence-based decision-making.

---

# 📂 Evidence Summary

| Evidence | Status |
|----------|--------|
| Email Headers | ✅ Collected |
| Sender Information | ✅ Verified |
| SPF Authentication | ✅ Reviewed |
| Base64 Content | ✅ Decoded |
| Attachment Analysis | ✅ Completed |
| File Signature Validation | ✅ Completed |
| Archive Extraction | ✅ Completed |
| Hidden Spreadsheet | ✅ Recovered |
| Metadata Analysis | ✅ Completed |
| Indicators of Compromise | ✅ Documented |
| Investigation Report | ✅ Completed |

---

# 📈 Project Outcomes

✔ Successfully analyzed a suspicious phishing email.

✔ Validated sender authenticity through email header analysis.

✔ Identified failed SPF authentication.

✔ Verified the attachment's true file type.

✔ Extracted concealed evidence from a disguised archive.

✔ Recovered hidden Base64-encoded information.

✔ Documented actionable Indicators of Compromise (IOCs).

✔ Produced a structured incident report using SOC investigation methodology.

---

# 🛡 Security Recommendations

Based on the evidence collected throughout this investigation, the following recommendations are proposed to strengthen email security controls and reduce the risk of similar phishing attacks and improve the organization's overall email security posture.


| Recommendation | Security Benefit |
|----------------|------------------|
| Enforce SPF, DKIM, and DMARC | Prevent email spoofing and improve sender verification. |
| Deploy Advanced Email Security Gateways | Detect malicious attachments, spoofed emails, and suspicious URLs before delivery. |
| Verify File Signatures | Validate files using magic numbers rather than relying on file extensions. |
| Block Known Indicators of Compromise | Restrict communications from identified malicious domains, hosts, and IP addresses. |
| Conduct Regular Security Awareness Training | Improve users' ability to recognize phishing attempts and suspicious attachments. |
| Investigate Authentication Failures | Monitor SPF, DKIM, and DMARC failures for potential phishing campaigns. |
| Analyze Attachments in Sandboxed Environments | Prevent malicious files from executing on production systems. |
| Preserve Digital Evidence | Maintain evidence integrity for future forensic investigations and incident response activities. |

---

# 📊 Risk Assessment

| Category | Assessment |
|----------|------------|
| Threat Type | Phishing |
| Initial Access Technique | Malicious Email Attachment |
| Risk Level | Medium |
| Business Impact | Moderate |
| User Interaction Required | Yes |
| Evidence Integrity | Preserved |
| Investigation Status | Complete |

---

# 🧠 Lessons Learned

This investigation reinforced several fundamental principles of phishing analysis and digital forensics.

- Email authentication failures should always be investigated alongside other indicators rather than in isolation.
- File extensions should never be trusted without validating the underlying file signature.
- Base64 encoding is frequently used to conceal malicious or suspicious content during email transmission.
- Hidden files and concealed spreadsheet data may contain valuable forensic evidence.
- Document metadata can provide investigative leads but should never be relied upon for definitive attribution.
- Correlating multiple artifacts produces stronger investigative conclusions than relying on a single indicator.
- Proper documentation is essential for effective incident response and knowledge sharing.

---

# 🎯 Skills Demonstrated

## Security Operations

- Phishing Email Investigation
- Threat Analysis
- Security Monitoring
- IOC Identification
- Incident Documentation
- Digital Evidence Collection

---

## Digital Forensics

- Email Header Analysis
- SPF Validation
- Base64 Decoding
- File Signature Verification
- Metadata Analysis
- Hidden File Discovery
- Archive Analysis

---

## Technical Skills

- Windows 11 Virtual Machine
- File System Investigation
- Evidence Preservation
- Structured Incident Reporting
- Analytical Problem Solving
- Cybersecurity Documentation

---

# 📚 What This Project Demonstrates

This project showcases my ability to perform a structured phishing investigation using methodologies aligned with Security Operations Center (SOC) workflows.

Throughout the investigation, I successfully:

- Investigated a suspicious phishing email.
- Validated sender authenticity through email header analysis.
- Identified authentication failures and spoofing indicators.
- Determined the true nature of a disguised attachment.
- Decoded concealed Base64 content.
- Recovered hidden forensic evidence.
- Documented Indicators of Compromise (IOCs).
- Produced a professional incident report suitable for security operations documentation.

This project reflects the investigative, analytical, and documentation skills expected of an entry-level SOC Analyst.

--

# 🚀  Future Improvements
As I continue developing my SOC and DFIR skills, I plan to extend this investigation by implementing:

- Microsoft Sentinel detection rules.
- Splunk search queries for phishing detection.
- Sigma detection rules.
- YARA rules for suspicious attachments.
- Threat intelligence enrichment of Indicators of Compromise.
- Automated email header analysis using Python.
- Email sandbox analysis for suspicious attachments.
- Malware reverse engineering (where applicable).


---

# 📖 References

- MITRE ATT&CK Framework
- Microsoft Security Documentation
- Google Cybersecurity Professional Certificate
- Digital Forensics Best Practices
- Sender Policy Framework (SPF) Documentation

---

# 🌟 Final Reflection

Cybersecurity is about more than identifying malicious activity—it's about understanding attacker behavior, validating evidence, communicating findings effectively, and continuously improving defensive capabilities.

This investigation strengthened my ability to think like a SOC Analyst by applying structured investigative techniques, documenting evidence, and producing a professional incident report based on real-world methodologies.

I am passionate about investigating security incidents, analyzing threats, and continuously developing hands-on cybersecurity skills through practical labs and real-world projects.

My goal is to build a career in Security Operations, Incident Response, Threat Detection, and Cloud Security while contributing to organizations by protecting systems against evolving cyber threats.

Every investigation is an opportunity to learn, improve, and become better prepared for the next threat.

---

<div align="center">

# Thank You for Visiting This project

### If you found this project insightful or helpful, please consider giving it a ⭐.

### Feedback, suggestions, and professional connections are always welcome.

**"Continuous learning, practical experience, and disciplined investigation are the foundation of every successful cybersecurity professional."**

---

**Built with curiosity, integrity, and a passion for SOC Analysis.**

</div>
