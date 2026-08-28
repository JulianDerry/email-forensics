# Email Forensics

Email authentication and phishing investigation work covering headers, delivery paths, SPF, DKIM, DMARC, URL analysis, and evidence validation.

Part of the **JulianDerry DFIR portfolio**.

## Overview

Email remains one of the most common intrusion vectors, and one of the easiest artifacts to misread if the header chain is not fully reconstructed.

This repository documents phishing and email authentication investigations, tracing routing paths, validating sender authentication records, and separating what a header actually proves from what it merely suggests.

## Case Index

| Investigation | What it covers | Status | Link |
|---|---|---|---|
| Phishing Email Investigation | Full header reconstruction, sender identity, SPF, DKIM, DMARC, embedded URL and VirusTotal analysis, timeline validation | Complete | [Go to Phishing Email Investigation](phishing-email-investigation) |

## Planned Coverage

Areas the portfolio is expanding into. These become case index rows once a folder exists for each.

### Email Header Analysis

Analysis and reconstruction of email headers to establish message origin, routing information, authentication results, and relevant metadata.

### Delivery Path Reconstruction

Reconstruction and analysis of the sequence of mail servers involved in message delivery.

### Sender and Domain Analysis

Analysis of sender identity, domains, authentication alignment, and related indicators.

### Attachment Analysis

Forensic examination of email attachments and associated metadata.

### Automated SPF, DKIM, and DMARC Parsing Tooling

Development and use of tooling to automate the parsing and validation of SPF, DKIM, and DMARC authentication results.

## Methodology

```text
Identification
      |
Preservation
      |
Acquisition
      |
Hash Verification
      |
Examination
      |
Analysis
      |
Correlation
      |
Timeline Reconstruction
      |
Reporting
```
Header data is cross-checked against the raw message source in every case; nothing is reported from a parsed summary alone.

## Toolkit

- Gmail
- Header analysis tooling
- SPF validation
- DKIM validation
- DMARC validation
- VirusTotal

## Evidence and Reporting Standard

Each investigation in this repository documents:

- Acquisition method and chain of custody
- Hash verification
- Header and routing examination
- What the evidence established
- What the evidence did not establish
- Limitations and considerations

## Investigative Scope

Investigations in this repository are conducted on training datasets, lab environments, or authorized evidence sources for educational and professional portfolio purposes.

Portfolio material does not represent confidential client evidence.

## Contact

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/julian-derry-936271312/) [![X](https://img.shields.io/badge/X-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/CyberSamuraiDev)
