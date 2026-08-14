# Phishing Email Forensic Investigation

| Field | Value |
|---|---|
| **Case Reference** |DFIR-2026-EMAIL-001  |
| **Analyst** | Julian Derry |
| **Date of Analysis** | ‎August 14, 2026 |
| **Evidence Source:** | Suspicious email delivered to `xxxxxx@gmail.com` |
| **Tools** | Gmail, Email Header Analysis, SPF/DKIM/DMARC Validation, VirusTotall |

---

## Objective

Authenticate a suspicious email by examining message headers, sender identity, mail routing path, SPF, DKIM, DMARC, embedded URLs, and overall phishing indicators.

---

## Evidence Preservation

- Exported the email from Gmail as a `.eml` file.
- Preserved the original message in read-only form.
- Verified associated file hashes.

**Evidence File:** `blocked email.eml`

| Hash Type | Value |
|---|---|
| SHA256 | `021bedb7c722674260f54ddd5f3d05306c5f4ce035d9df4913dee52018bd5416` |
| MD5 | `72c1199ffa543d8995f03439ad571fed` |

### Screenshot 1 – Exported EML File and Hash Values

<img width="1206" height="670" alt="Screenshot 2026-08-14 103618" src="https://github.com/user-attachments/assets/c297df75-067d-46b2-bd56-5724d3e50ee0" />
<img width="1109" height="476" alt="Screenshot 2026-08-14 104606" src="https://github.com/user-attachments/assets/287a1323-c846-4216-97d7-d275c794dc1f" />

---

## Claimed Sender Analysis

**From:** `twsupportvtg@xgsesqbyqzbydblvkhnodfqh.com`  
**Return-Path:** `abuse@monitoring-reporting.overview.commerce.gov.accordinant.com`  
**Reply-To:** `reply@iwzu1.c7gbvvg.uic.edu`

**Finding:** The sender domains do not match, indicating identity inconsistency.

### Screenshot 2 – From, Return-Path and Reply-To Headers

<img width="1919" height="1031" alt="Initial assessment" src="https://github.com/user-attachments/assets/5a7ccce2-c5e3-498b-8533-27782ff3de31" />

---

## Delivery Path Verification

The earliest external server identified in the Received headers was:

- `gerhold.dividnovic.com (66.165.231.172)`

**Finding:** The message was received from a third-party host rather than Google mail infrastructure.

### Screenshot 3 – Received Headers

<img width="1919" height="1031" alt="delivery path" src="https://github.com/user-attachments/assets/5a13b25a-8979-433c-aa0c-cd2e0d99f8ce" />

---

## SPF Validation

**Result:** `spf=pass`

SPF passed for the envelope sender domain but not for the visible From domain.

**Finding:** SPF does not authenticate the visible sender address.

### Screenshot 4 – SPF Result

<img width="1919" height="1031" alt="SPF Check" src="https://github.com/user-attachments/assets/6eeff75d-df01-4837-9b76-5b6592e15684" />

---

## DKIM Validation

**DKIM Domain:** `xgsesqbyqzbydblvkhnodfqh.com`  
**Result:** `dkim=permerror (no key for signature)`

**Finding:** DKIM verification failed because no valid public key was available.

### Screenshot 5 – DKIM Signature and Result

<img width="1919" height="1031" alt="DKIM Check" src="https://github.com/user-attachments/assets/75024cae-d3df-45dd-b181-5cc74e6470c3" />

---

## DMARC Evaluation

DMARC requires aligned SPF or aligned DKIM.

- SPF alignment: **Fail**
- DKIM alignment: **Fail**

**Finding:** DMARC authentication failed.

### Screenshot 6 – DMARC Evaluation

<img width="1919" height="1031" alt="Determine DMARC status" src="https://github.com/user-attachments/assets/c6916560-8c7d-4242-9a88-f3914e7e61b6" />

---

## Phishing Content Indicators

**Subject:** *We've blocked your account! Your photos and videos will be deleted...*

Observed indicators:

- Urgent language
- Threat of account deletion
- Security scare tactics
- Immediate action request

**Finding:** Strong phishing characteristics present.

### Screenshot 7 – Email Subject and Body

<img width="1918" height="1031" alt="Evaluate header consistency" src="https://github.com/user-attachments/assets/14d69ab4-88ed-423e-ac72-42183bcd90c3" />

---

## URL Inspection

Example embedded URL:

```text
http://storage.googleapis.com/salmonnais/5EArrondissement.html#/redirect.html
```

Observations:

- Uses **HTTP** rather than HTTPS.
- Hosted on a cloud storage service.
- Destination unrelated to the claimed sender.
- Reported as malicious by VirusTotal.

**Finding:** Malicious or deceptive URL identified.

### Screenshot 8 – Embedded URL and VirusTotal Result

<img width="1918" height="1031" alt="Embedded URL" src="https://github.com/user-attachments/assets/171ff3d9-d341-473c-9ded-16821d0e91c0" />

---

## Domain Correlation

| Purpose | Domain |
|---|---|
| Visible Sender | `xgsesqbyqzbydblvkhnodfqh.com` |
| Envelope Sender | `monitoring-reporting.overview.commerce.gov.accordinant.com` |
| Reply-To | `uic.edu` |
| Sending Host | `dividnovic.com` |
| Link Host | `storage.googleapis.com` |

**Finding:** Multiple unrelated domains are present in a single message, which is consistent with phishing activity.
---

## Timeline Validation

| Event | Timestamp |
|---|---|
| Message Created | Fri, 31 Jul 2026 05:40:38 -0400 |
| Received by Gmail | Fri, 31 Jul 2026 02:42:08 -0700 |

The timestamps are internally consistent when converted to UTC.

**Finding:** No timestamp anomaly detected.
---

# Authentication Summary

| Control | Result |
|---|---|
| SPF | Pass |
| DKIM | Fail |
| DMARC | Fail |
| From Alignment | Fail |
| Reply-To Consistency | Fail |
| Sending Infrastructure | Fail |
| URL Analysis | Fail |

---

# Conclusion

The email **cannot be authenticated as a legitimate Gmail communication**. The visible sender identity is not supported by SPF, DKIM verification failed, DMARC alignment failed, and the message contains multiple phishing indicators including deceptive URLs and urgent account-deletion language.

**Final Classification:** **PHISHING / MALICIOUS EMAIL**

## Skills Learned

- Email evidence acquisition and preservation
- Exporting and handling `.eml` files
- File hash verification (SHA256 and MD5)
- Email header analysis
- Sender identity verification
- From, Return-Path, and Reply-To analysis
- Mail routing and Received header analysis
- Source IP identification and attribution
- SPF record validation and interpretation
- Understanding SPF alignment limitations
- DKIM signature analysis
- DKIM failure and `permerror` interpretation
- DMARC evaluation and alignment analysis
- Email authentication correlation
- Phishing indicator identification
- Social engineering content assessment
- Malicious URL inspection
- Cloud-hosted phishing link analysis
- VirusTotal URL reputation analysis
- Multi-domain correlation and spoofing detection
- Email timeline validation and timestamp analysis
- Evidence documentation and forensic reporting
- Digital forensic analytical reasoning
- Phishing email classification and conclusion writing
