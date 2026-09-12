# Case #2 — Binance Fake Withdrawal Notification

**Date Investigated:** [Investigation Date]
**Analyst:** Amina Sheikh
**Severity:** Critical
**TLP:** TLP:AMBER

## Email Details

- **Subject:** [Binance] Withdraw Successful - 2023-07-30
- **Sender (Displayed):** Binance
- **Sender (Actual):** noreply-supportbinancewallet.irs@auswestbc.com.au
- **Sending Infrastructure:** Amazon SES (eu-central-1.amazonses.com)
- **Received Date:** July 30, 2023

## Technical Analysis

| Check | Result |
|---|---|
| SPF | Pass (for amazonses.com) |
| DKIM | Pass (verified, signed by amazonses.com) |
| DMARC | None (no policy enforced) |
| Sender IP | 69.169.224.12 |
| SPF/DKIM Authenticated Domain | amazonses.com |
| Claimed Sender Domain | auswestbc.com.au (does not match binance.com) |

## Content Analysis

- Notifies the recipient of a "successful" cryptocurrency withdrawal 
  (0.5436303557445 ETH) they did not initiate
- Uses fear-based urgency: "Don't recognize this activity? Please cancel 
  this transaction..."
- Includes a "Cancel Transaction" button linking to an external domain 
  disguised as an official Binance security action
- Mimics Binance's official branding, logo, and email template styling to 
  appear legitimate
- Ironically includes a genuine-looking Binance phishing warning footer 
  ("Please be aware of phishing sites...") to further build false trust

## IOCs (Indicators of Compromise)

| Type | Value |
|---|---|
| Sender Email | noreply-supportbinancewallet.irs@auswestbc.com.au |
| Claimed Domain | binance.com (impersonated) |
| Actual Sender Domain | auswestbc.com.au |
| Sending Infrastructure | eu-central-1.amazonses.com |
| Sender IP | 69.169.224.12 |
| Malicious Link | hxxps://shylshom[.]com/ |

## Attack Technique Identified

**Brand impersonation via legitimate email infrastructure abuse** — the 
attacker used Amazon SES, a legitimate bulk email service, to send a 
spoofed notification impersonating Binance, directing victims to a fake 
"cancel transaction" link designed to harvest credentials or trigger 
fraudulent account actions.

## Verdict

**Classification:** True Positive — Confirmed Phishing

## Reasoning

1. The email claims to be from Binance, but the actual sending domain is 
   auswestbc.com.au, an unrelated domain with no connection to Binance's 
   official infrastructure (binance.com).
2. SPF and DKIM both passed, but only for amazonses.com, the third-party 
   email service used to send the message, not for Binance or the claimed 
   sending domain. A passing authentication result confirms the sending 
   infrastructure is legitimate, not that the sender's identity claim is 
   true. Attackers can rent legitimate bulk-mail services specifically to 
   bypass basic spam filtering.
3. DMARC returned "none," meaning there is no enforced policy to reject 
   or quarantine messages that fail domain alignment, allowing this 
   spoofed message through.
4. The "Cancel Transaction" button links to shylshom.com, a domain with 
   no relation to Binance's official website.
5. The email uses a classic fear-based social engineering hook (an 
   unauthorized withdrawal) to pressure the recipient into clicking 
   immediately without verifying.
6. The inclusion of a legitimate-looking anti-phishing warning within the 
   email itself is a deliberate tactic to increase perceived credibility.

## Recommended Actions

- [ ] Block the sending domain (auswestbc.com.au) and malicious URL 
      (shylshom.com) at the email/web gateway
- [ ] Report the abuse of Amazon SES infrastructure to AWS Trust & Safety
- [ ] Issue a user awareness alert regarding fake Binance/crypto exchange 
      notifications
- [ ] No further action needed as this was not delivered to a live 
      production mailbox

## Key Learning

This case highlights an important distinction from Case #1: passing SPF 
and DKIM checks does not automatically mean an email is safe. These 
checks only validate that the sending server was authorized to send on 
behalf of the domain it authenticated against, in this case, Amazon SES's 
own domain, not Binance. Verifying the actual sending domain against the 
claimed brand identity remains essential, even when authentication 
results appear clean.

---
*Sample sourced from a public phishing research dataset for educational 
investigation purposes.*
