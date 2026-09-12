# Phishing Email Investigation

## Overview

Hands-on investigation of real-world phishing samples, applying the same 
methodology used by SOC analysts to triage suspicious emails: header 
analysis, authentication verification (SPF/DKIM/DMARC), sender legitimacy 
checks, and IOC extraction.

Samples were sourced from publicly available phishing research datasets, 
used strictly for educational investigation purposes.

## Methodology

Each email was investigated using the following process:

1. **Header Extraction** — Full email headers reviewed for routing 
   information, sender IP, and authentication results.
2. **Authentication Verification** — SPF, DKIM, and DMARC results 
   validated using MXToolbox's Email Header Analyzer.
3. **Sender Legitimacy Check** — Displayed sender name compared against 
   the actual sending domain to identify impersonation.
4. **Content Analysis** — Reviewed for urgency tactics, generic greetings, 
   grammar issues, and requests for money or personal information.
5. **Link/IOC Verification** — Any embedded links or IP addresses checked 
   against VirusTotal for reputation data.
6. **Verdict & Documentation** — Findings compiled into a structured case 
   report following an industry-style incident format (TLP classification, 
   IOC table, recommended actions).

## Cases Investigated

| Case | Type | Verdict | Key Technique |
|---|---|---|---|
| [Case 1](./Case1_Lottery_Scam.md) | Advance-Fee Fraud | True Positive | Sender domain impersonation, failed DMARC |
| [Case 2](./Case2_Binance_Fake_Withdrawal.md) | Credential/Fraud Scam | True Positive | Legitimate email service abuse (Amazon SES), fake domain link |

## Key Takeaway

The two cases investigated here represent two different levels of 
sophistication. The first was identifiable through failed authentication 
checks alone. The second showed passing SPF and DKIM results, at first 
glance a sign of legitimacy, until closer inspection revealed those checks 
only validated the sending infrastructure (Amazon SES), not the claimed 
sender (Binance). 

This reinforced an important principle in email investigation: a passing 
authentication result confirms the sending service is legitimate, not that 
the sender's identity claim is true. Domain matching and link verification 
remain essential even when technical checks look clean.

## Tools Used

- MXToolbox (Email Header Analyzer)
- VirusTotal
- Manual header inspection

---
*Samples used for educational investigation purposes only.*
