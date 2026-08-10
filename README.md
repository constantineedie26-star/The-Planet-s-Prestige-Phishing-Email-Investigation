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

The extracted archive contained a folder named `PuzzleToCoCanDa`.
![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/74a69a76ce4953130d8877a74607ed54267977a3/Puzzletococanda.png)

Upon extraction, the archive contained two files-`DaughtersCrown` and GoodJobMajor`-`which were identified for further forensic analysis.
![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/74a69a76ce4953130d8877a74607ed54267977a3/Daughters%20crown%20and%20goodjobmajor.png)
---


# Phase 7-Hidden File Analysis

## Objective

Tdentify concealed evidence contained within the extracted archive.

## Investigation

The extracted archive contained a folder named `PuzzleToCoCanDa`. Initial inspection revealed two visible files-`DaughtersCrown and GoodJobMajor`. After enabling Hidden items in File Explorer, a hidden spreadsheet `(Money.xlsx)` was also identified. Before opening any files, their actual file types and contents were verified as part of the forensic investigation.

Further analysis revealed concealed Base64-encoded information embedded within the spreadsheet.

While reviewing the extracted folder, I enabled Hidden items in Windows File Explorer. This revealed an additional file named Money.xlsx that was not visible by default.


![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/3525123a91b105b3be9be101f9c2119d2c5a0fd2/Hidden%20File%20discovery.png)


| File Name | Visibility | Initial Assessment |
|-----------|------------|--------------------|
| `DaughtersCrown` | Visible | Identified for subsequent file-type verification and analysis. |
| `GoodJobMajor` | Visible | Flagged for further examination to determine its contents and purpose. |
| `Money.xlsx` | Hidden | Discovered after enabling **Hidden items** in File Explorer. Its concealed status elevated its priority for detailed file-type and content analysis. |

> **Observation:** The archive contained three files. The presence of the hidden file `Money.xlsx` suggested a deliberate attempt to conceal information, making it a high-priority artifact for further forensic investigation.


Hidden files and concealed data are common techniques used to delay detection and complicate forensic investigations.

---

# Phase 8-Extracted File Analysis

#### `DaughtersCrown`

The extracted file, `DaughtersCrown`, was saved without a file extension. To determine its true file type, I examined its file signature using **HxD Hex Editor** before opening the file.

Analysis revealed the hexadecimal signature:

`FF D8 FF E0`

Cross-referencing this signature with **Gary Kessler's File Signature Table** confirmed that it corresponds to a **JPEG/JFIF image**, verifying the file as a standard JPEG image despite the absence of a file extension.

| **Attribute** | **Value** |
|:--------------|:----------|
| **File Name** | `DaughtersCrown` |
| **File Extension** | None |
| **Analysis Tool** | `HxD Hex Editor` |
| **Observed File Signature** | `FF D8 FF E0` |
| **Identified File Type** | `JPEG/JFIF Image` |
| **Reference** | Gary Kessler's File Signature Table |
| **Finding** | File-signature analysis confirmed that the file is a legitimate JPEG/JFIF image despite having no file extension. |

The file was analyzed in HxD Hex Editor to verify its true file type. Examination of the file header revealed the hexadecimal signature `FF D8 FF E0`, providing the evidence needed for file-type identification.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/afb00fae2a60760f5e87f05626a07ecc320c9648/HxD%20Hex%20Editor.png)

The identified file signature was validated against Gary Kessler's File Signature Table, confirming a match with the standard JPEG/JFIF signature. This verification established the file's true format independently of its missing file extension

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/afb00fae2a60760f5e87f05626a07ecc320c9648/Gary%20Kessler's%20File%20Signature%20Table.png)

Following successful file-signature verification, I renamed DaughtersCrown to DaughtersCrown.jpeg so that its filename accurately represented its verified JPEG format, facilitating subsequent analysis.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/010a06c9ce8815dddfdca40547da9b6438d9665d/DaughtersCrown-jpeg.png)

After confirming the file's true format through file-signature analysis, I opened DaughtersCrown.jpeg within the isolated Windows 11 virtual machine. The file rendered successfully and displayed a crown graphic, confirming that the renamed file was a valid JPEG image.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/010a06c9ce8815dddfdca40547da9b6438d9665d/DaughtersCrown.png)

### 🖼️ DaughtersCrown Findings

| **Attribute** | **Finding** |
|:--------------|:------------|
| **Original Filename** | `DaughtersCrown` |
| **Original Extension** | None |
| **Observed File Signature** | `FF D8 FF E0` |
| **Identified File Type** | `JPEG/JFIF Image` |
| **Renamed File** | `DaughtersCrown.jpeg` |
| **Observed Content** | A crown image was successfully rendered after renaming the file, confirming that it was a valid JPEG image. |
| **Conclusion** | File-signature analysis verified that the file was a legitimate JPEG/JFIF image despite having no file extension. |



#### `GoodJobMajor`

The extracted file, `GoodJobMajor`, was saved without a file extension. To determine its true file type, I examined its file signature using **HxD Hex Editor** before opening the file.

Analysis of the file header revealed the following hexadecimal signature:

`25 50 44 46`

Cross-referencing this signature with **Gary Kessler's File Signature Table** confirmed that it corresponds to a **Portable Document Format (PDF)** file. This verification established the file's true format despite the absence of a file extension.

After validating the file type, I renamed `GoodJobMajor` to `GoodJobMajor.pdf` so that its filename accurately reflected its verified format.

The renamed file was then opened within the isolated Windows 11 virtual machine. Examination confirmed that it contained a PDF document with additional instructions related to the investigation.

### 📄 GoodJobMajor Findings

| **Attribute** | **Finding** |
|:--------------|:------------|
| **Original Filename** | `GoodJobMajor` |
| **Original Extension** | None |
| **Analysis Tool** | `HxD Hex Editor` |
| **Observed File Signature** | `25 50 44 46` |
| **Identified File Type** | `Portable Document Format (PDF)` |
| **Reference** | Gary Kessler's File Signature Table |
| **Renamed File** | `GoodJobMajor.pdf` |
| **Observed Content** | PDF document containing additional instructions related to the investigation. |
| **Conclusion** | File-signature analysis confirmed that the file was a legitimate PDF document despite having no file extension. |

The file was analyzed in HxD Hex Editor to verify its true file type. Examination of the file header revealed the hexadecimal signature 25 50 44 46, providing the evidence required to accurately identify the file as a PDF document.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/5bf5fb048e3584883d6fb536e4828e1c8e372ec6/GoodJobMajor%20HxD.png)

The identified file signature was cross-referenced with Gary Kessler's File Signature Table, confirming a match with the standard PDF signature. This validation established the file's true format independently of its missing file extension.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/5bf5fb048e3584883d6fb536e4828e1c8e372ec6/GoodJobMajor%20kessler.png)

Following successful file-signature verification, I renamed `GoodJobMajor` to `GoodJobMajor.pdf` so that its filename accurately reflected its verified PDF format, facilitating subsequent analysis.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/741fb1a071e574950784e9ecbb362c2c2cf49c23/GoodJobMajor-pdf.png)

After confirming the file's true format through file-signature analysis, I opened GoodJobMajor.pdf within the isolated Windows 11 virtual machine. The document revealed that the CoCanDians were safe, referenced DaughtersCrown as supporting evidence, and instructed the recipient to consult Money.xlsx for the destination associated with the 1 Billion CoCanDs payment. This finding identified Money.xlsx as the next key artifact for forensic analysis.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/741fb1a071e574950784e9ecbb362c2c2cf49c23/GoodJobMajor%20content.png)

### 📄 GoodJobMajor Findings

| **Attribute** | **Finding** |
|:--------------|:------------|
| **Original Filename** | `GoodJobMajor` |
| **Original Extension** | None |
| **Observed File Signature** | `25 50 44 46` |
| **Identified File Type** | `Portable Document Format (PDF)` |
| **Renamed File** | `GoodJobMajor.pdf` |
| **Observed Content** | The document stated that the CoCanDians were safe, referenced `DaughtersCrown` as supporting evidence, and directed the investigation to `Money.xlsx` for the location associated with the 1 Billion CoCanDs payment. |
| **Conclusion** | File-signature analysis confirmed that the file was a legitimate PDF document despite having no file extension. The document also identified `Money.xlsx` as the next critical artifact for further forensic investigation. |



----
# Phase 9-Metadata Analysis

## Objective

To identify additional forensic artifacts, I examined the metadata of GoodJobMajor.pdf using ExifTool. Analysis of the document's Author field revealed the first and last name requested during the investigation, demonstrating how document metadata can provide valuable investigative leads.

## Investigation

### 📋 Metadata Findings

| **Attribute** | **Finding** |
|:--------------|:------------|
| **Analyzed File** | `GoodJobMajor.pdf` |
| **Analysis Tool** | `ExifTool` |
| **Author** | `Pestero Negeja` |
| **Producer** | `Skia/PDF m90` |
| **Page Count** | `1` |
| **Finding** | The `Author` metadata field contained the name **Pestero Negeja**, providing the first and last name requested during the investigation. |

> **Observation:** Document metadata identified **Pestero Negeja** as the likely creator of the PDF. However, metadata can be modified and should be treated as an investigative lead rather than conclusive evidence of authorship.

Metadata should always be corroborated with additional evidence.


#### `Money.xlsx`

Although the hidden file `Money.xlsx` already had a valid file extension, I verified its true file type through file-signature analysis before opening it. Using **HxD Hex Editor**, I examined the file header to confirm that its contents matched the declared spreadsheet format.

Analysis of the file header revealed the following hexadecimal signature:

`50 4B 03 04`

The recovered file signature was cross-referenced with **Gary Kessler's File Signature Table**, where it matched the standard signature used by **Microsoft Office Open XML** documents, including `.xlsx` spreadsheets. This verification confirmed that the file was a legitimate Microsoft Excel workbook.

After validating the file type, I safely opened `Money.xlsx` within the isolated Windows 11 virtual machine for further forensic analysis.

### 📊 Money.xlsx Findings

| **Attribute** | **Finding** |
|:--------------|:------------|
| **Filename** | `Money.xlsx` |
| **Visibility** | Hidden |
| **Analysis Tool** | `HxD Hex Editor` |
| **Observed File Signature** | `50 4B 03 04` |
| **Identified File Type** | `Microsoft Office Open XML Spreadsheet (.xlsx)` |
| **Reference** | Gary Kessler's File Signature Table |
| **Status** | Successfully verified and opened for further analysis. |
| **Conclusion** | File-signature analysis confirmed that `Money.xlsx` was a legitimate Microsoft Excel workbook. Despite having a valid file extension, independent verification ensured that the file matched its declared format before examination. |

The file was examined in HxD, where the first four bytes of the file header were identified as 50 4B 03 04.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/2d83bd898bda08079f2402d69934a69550c15e0d/money%20HxD.png)

The identified file signature was compared against Gary Kessler’s File Signature Database and confirmed to correspond to the Microsoft Office Open XML format used by `.xlsx` spreadsheet files.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/2d83bd898bda08079f2402d69934a69550c15e0d/Money%20Kessler.png)

After verifying the file signature, I safely opened Money.xlsx in googlesheet within an isolated Windows VM. The first worksheet revealed a message contradicting the earlier intelligence and threatening to initiate war against the CoCanDians.

Security Note: `The spreadsheet was analyzed in an isolated environment to reduce the risk associated with handling an untrusted file`.

Money.xlsx first worksheet:

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/2d83bd898bda08079f2402d69934a69550c15e0d/Money%20sheet%201.png)

A second worksheet, `Sheet3`, initially appeared blank. After removing the cell formatting, previously concealed text was revealed, providing an additional investigative clue.

Hidden text discovery in Sheet3.The worksheet initially appeared blank.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/2d83bd898bda08079f2402d69934a69550c15e0d/Blank%20Worsheet3.png)


Clearing the formatting revealed a previously concealed **encoded string**, providing an additional clue for further analysis.

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/2d83bd898bda08079f2402d69934a69550c15e0d/Encoded%20String.png)

#### Base64 Decoding

The concealed string recovered from `Sheet3` was copied into **CyberChef** and decoded using the **From Base64** operation, revealing the underlying message for further analysis.

**Base64 Decoding of the Concealed `Sheet3` Text**

![image alt](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/2d83bd898bda08079f2402d69934a69550c15e0d/Base64%20sheet%203.png)


The decoded message revealed the location: `The Martian Colony, Beside Interplanetary Spaceport.`

This finding confirmed the location referenced in `GoodJobMajor.pdf` and provided the next investigative lead.

#### `Money.xlsx` Findings

* **Filename:** `Money.xlsx`
* **File Signature:** `50 4B 03 04`
* **Verified File Type:** Microsoft Excel Open XML spreadsheet
* **Worksheets:** `Sheet1`, `Sheet3`
* **`Sheet1`:** Contained a message disputing the earlier intelligence and threatening war against the CoCanDians.
* **`Sheet3`:** Contained Base64-encoded text concealed through cell formatting.
* **Decoded Location:** `The Martian Colony, Beside Interplanetary Spaceport.`

## 🔎 Findings Summary

The investigation began with a suspicious `.eml` email containing a ransom-themed message and an attachment disguised as `PuzzleToCoCanDa.pdf`.

### 🚨 Initial Indicators of Compromise

Email-header analysis uncovered multiple red flags:

* **SPF authentication:** Failed
* **Sender vs. Reply-To:** Different domains, indicating potential spoofing or impersonation
* **Attachment:** Base64-encoded and falsely presented as a PDF
* **File signature:** Confirmed the attachment was actually a ZIP-based archive

### 🧩 Artifact Extraction & Analysis

After safely decoding and extracting the archive within an **isolated Windows virtual machine**, three artifacts were recovered:

| Artifact         | Identified Type   | Key Finding                                     |
| ---------------- | ----------------- | ----------------------------------------------- |
| `DaughtersCrown` | JPEG image        | Image depicting a crown                         |
| `GoodJobMajor`   | PDF document      | Contained additional investigative instructions |
| `Money.xlsx`     | Excel spreadsheet | Hidden file containing encoded content          |

Further analysis of `Money.xlsx` revealed a concealed Base64-encoded message hidden through spreadsheet formatting.

### 🔐 Decoded Intelligence

The concealed Base64 content was extracted and decoded using **CyberChef**, revealing the following location:

```text
The Martian Colony, Beside Interplanetary Spaceport.
```

This became the **final investigative lead** uncovered from the malicious email and its associated artifacts.

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

## 🧠 Investigation Conclusion

The investigation demonstrated a multi-layered attempt to conceal malicious content through **sender spoofing, failed email authentication, deceptive file extensions, encoded data, archive masquerading, hidden files, and spreadsheet-based obfuscation**.

By systematically analyzing the raw email, validating file signatures, decoding Base64 content, extracting the disguised archive, and examining the recovered artifacts, I successfully traced the attacker’s embedded instructions to:

```text
The Martian Colony, Beside Interplanetary Spaceport.
```

The investigation findings were successfully validated against the **Blue Team Labs Online** challenge, confirming completion of **The Planet’s Prestige** investigation.


> **Key Takeaway:** This investigation reinforced the importance of validating email headers, file signatures, encoded content, and hidden artifacts rather than trusting filenames, extensions, or visible email content at face value.

# Thank You for Visiting This project

### If you found this project insightful or helpful, please consider giving it a ⭐.

### Feedback, suggestions, and professional connections are always welcome.

**"Continuous learning, practical experience, and disciplined investigation are the foundation of every successful cybersecurity professional."**

---

**Built with curiosity, integrity, and a passion for SOC Analysis.**

## 🏆 Challenge Completion

**Challenge:** The Planet’s Prestige
**Platform:** Blue Team Labs Online
**Status:** ✅ Successfully Completed
**Completion Date:** August 10, 2026
![Image](https://github.com/constantineedie26-star/The-Planet-s-Prestige-Phishing-Email-Investigation/blob/067d7426a9126fc1c9ca94a51c2c086871f2e118/Blue%20team%20challenge.png)

