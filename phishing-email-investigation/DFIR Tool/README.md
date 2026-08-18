
# MailTrace & Analyzer V1

**MailTrace & Analyzer** is a digital forensics tool developed to assist with the examination and analysis of `.eml` email evidence. The tool automates several repetitive parts of email header analysis and presents the results in a single forensic focused interface.

It analyzes the **Received header chain** to reconstruct the route an email took, identifies a potential **originating IP**, and provides an origin confidence assessment based on the available routing information. It also examines **SPF, DKIM, DMARC and ARC** authentication results and highlights potential anomalies such as differences between the `From` and `Return Path` domains or authentication failures.

The tool also provides **PTR/DNS and RDAP enrichment** to give additional context about the infrastructure associated with observed IP addresses. Each email is identified using its **SHA-256 hash**, and the application can process **up to 10 `.eml` files at a time**, allowing multiple messages to be examined and compared during an investigation.

MailTrace & Analyzer is intended to **assist the forensic analyst rather than replace manual examination**. An identified originating IP is treated as a network origin candidate and should not automatically be interpreted as proof of the physical sender or individual responsible for the email.

## V1 Features

- `.eml` file analysis
- Received chain reconstruction
- Originating IP candidate identification
- SPF, DKIM, DMARC and ARC analysis
- PTR/DNS enrichment
- RDAP/IP information enrichment
- Email anomaly detection
- SHA-256 evidence identification
- Batch analysis of up to 10 files
- Refresh and reload functionality
- Forensic analysis reports

## V2

**V2 is currently planned and will introduce additional visualization and analysis capabilities**, including displaying the **geographic location of the suspected originating IP and the individual hop IPs** identified throughout the email's routing path.

This will make it easier to visually understand the infrastructure and geographical path associated with an email and provide additional context during forensic examination.

**Developed by Julian Derry | MailTrace & Analyzer V1**
