# Case #1 — Lottery Winning Payment Scam

**Date Investigated:** [Investigation Date]
**Analyst:** Amina Sheikh
**Severity:** High
**TLP:** TLP:AMBER

## Email Details

- **Subject:** Lottery Winning payment
- **Sender (Displayed):** Royal Bank Of Canada
- **Sender (Actual):** RoyalBanlOfCannada@gmail.com
- **Reply-To:** rev.innocent-johnson27@outlook.com
- **Received Date:** August 1, 2023

## Technical Analysis (Verified via MXToolbox)

| Check | Result |
|---|---|
| DMARC Compliant | FAIL |
| SPF Alignment | Pass |
| SPF Authenticated | FAIL |
| DKIM Alignment | FAIL |
| DKIM Authenticated | FAIL |
| Sender IP | 187.217.4.86 |
| SPF Record Owner | gmail.com |
| DMARC Policy | p=none (monitor only, no enforcement) |
| Relay Delay | ~44 hours (unusually long) |

## Content Analysis

- Claims a $12,000,000 USD lottery prize tied to a "Coca-Cola Company" 
  promotional draw
- Requests an upfront "activation fee" of $320 USD to release the funds
- Uses formal, authoritative language ("The President and CEO") to build 
  false legitimacy
- Requests personal information (full name, address, phone number) under 
  the guise of prize delivery

## IOCs (Indicators of Compromise)

| Type | Value |
|---|---|
| Sender Email | RoyalBanlOfCannada@gmail.com |
| Reply-To Email | rev.innocent-johnson27@outlook.com |
| Sender IP | 187.217.4.86 |
| Contact Email (Scammer) | offiefdxebsjwme@gmail.com |

## Additional Verification

Sender IP (187.217.4.86) was checked on VirusTotal, no malicious flags 
were found. This does not change the verdict, since domain impersonation 
and failed email authentication (DMARC/DKIM) remain conclusive evidence 
of phishing. A clean IP reputation only means the sending infrastructure 
itself isn't currently flagged, not that the email is legitimate.

## Attack Technique Identified

**Advance-fee fraud (419 scam)** — a lottery winning notification 
requesting an upfront fee to release a fabricated prize.

## Verdict

**Classification:** True Positive — Confirmed Phishing/Scam

## Reasoning

1. The sender claims to be "Royal Bank Of Canada," a major financial 
   institution, but sends from a free Gmail address. Legitimate banks 
   send official communication from their own verified corporate domain, 
   never from consumer email providers.
2. DMARC authentication failed, confirming the message does not pass 
   domain-based authentication checks.
3. DKIM returned no signature at all, meaning there is no verification 
   that the email content is authentic or untampered.
4. SPF returned a failure for the sending IP, indicating that server was 
   not authorized to send on behalf of the domain it claims.
5. The email requests an upfront payment in exchange for a large lottery 
   prize, a hallmark of advance-fee fraud.
6. The Reply-To address differs from the From address, a common tactic 
   used to redirect victim responses to a separate attacker-controlled 
   inbox.
7. The relay delay of approximately 44 hours is inconsistent with normal 
   email delivery times, adding to the suspicious profile.

## Recommended Actions

- [ ] Block sender domain/IP at the email gateway
- [ ] Report sender address to abuse teams (Gmail, Outlook)
- [ ] No further action needed as this was not delivered to a live 
      production mailbox
- [ ] Use as a training example for phishing awareness

---
*Sample sourced from a public phishing research dataset for educational 
investigation purposes.*
