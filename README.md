# Analyze_A_Phishing_Email
A simple project to analyze phishing emails by identifying common signs like spoofed senders, fake links, and social engineering tactics. Useful for cybersecurity awareness, training, and email threat detection.

<img width="1920" height="1080" alt="Screenshot From 2025-09-23 14-03-08" src="https://github.com/user-attachments/assets/7a8f77aa-becc-43e0-bd99-075b403b5d09" />

# Analyze_A_Phishing_Email

Plain-text repository for analyzing a suspicious phishing email sample and documenting indicators, extraction steps, and remediation recommendations.

---

## Summary

This repository contains a plain-text analysis of a phishing email that impersonates a trusted brand (claims to be AAA). The sample exhibits multiple phishing indicators (spoofed sender, DMARC fail, likely mismatched links in HTML, template placeholders, etc.). The purpose of this repo is to store the raw sample, an analysis checklist, and safe instructions for extracting and verifying suspicious links.

---

## Files
<img width="1920" height="1080" alt="Screenshot From 2025-09-24 12-37-29" src="https://github.com/user-attachments/assets/8d0cb429-9e10-422d-be68-6a3d422e3734" />

 `Original message
Message ID	<4wvdi302-glfg5m4b-yln885zq-xhx7p5ad-qzmb9hon@convertkit-mail2.com>
Created on:	18 September 2025 at 02:27 (Delivered after 0 seconds)
From:	AAA_Emergency_Kit_Offer <hygdx@datastreamgalaxy.uk.net>
To:	vikaspalid2004@gmail.com
Subject:	vikaspalid2004! -Summer Must-Have – Free Car Emergency Kit ⚡. ID#2043
SPF:	PASS with IP 164.132.51.132 Learn more
DKIM:	'PASS' with domain 73f8lwldbx3.datastreamgalaxy.uk.net Learn more
DMARC:	'FAIL' Learn more`  
  Raw email headers and plain-text body (as collected). **Do not click any links** contained in HTML parts if you view the full `.eml`.

- `[mismatched_url_check.txt](http://datastreamgalaxy.uk.net/click?redirect=...)`  
  Notes on likely mismatched links and how to find them (hover, inspect `href` in HTML, search `href="` in `.eml`).

- `Issues:

"Sep 0, 2019" – Invalid date. There is no September 0.

"unsubscrib=" – Cut off, possibly due to improper encoding/wrapping. Should be “unsubscribe.`  
  Brief list of spelling/grammar issues found in the sample (e.g., `Sep 0, 2019`, truncated `unsubscrib=`).

- `Phishing traits found

Display-name spoofing
Sender shows AAA_Emergency_Kit_Offer (tries to look like AAA) while the actual sending domain is datastreamgalaxy.uk.net — classic impersonation.

Suspicious sending domain / Return-Path mismatch
Return-Path / From domains (datastreamgalaxy.uk.net, 73f8lwldbx3.datastreamgalaxy.uk.net) are unrelated to AAA and look random/throwaway.

DMARC failure (while SPF/DKIM pass)

SPF: PASS, DKIM: PASS, but DMARC: FAIL — indicates authentication is not aligned and the message is not authorized by the purported domain owner. Very suspicious.

Message-ID/domain spoofing
Message-ID uses convertkit-mail2.com while other headers use datastreamgalaxy.uk.net — inconsistent mail identities.

Unusual host / infrastructure hints
Mail received from 164.132.51.132 (OVH VPS / cloud host) and domains like cloudllineh.com.tr/zwimpad.com — often used by bulk/spam senders.

Urgency / reward social engineering in subject
Subject: vikaspalid2004! -Summer Must-Have – Free Car Emergency Kit ⚡. ID#2043 — personalized, urgent, “free” reward + emoji to trigger click-throughs.

Likely mismatched/hidden links (HTML part)
Email is multipart/alternative (plain + HTML). No links appear in the plain text, so malicious links are likely hidden in the HTML (display text that looks legitimate but href points to datastreamgalaxy... or tracking redirects).

Broken / suspicious content in body
Text body contains nonsense / placeholders: Sep 0, 2019, 103882302891885308, and a truncated unsubscrib= — indicates mass/template spam or poorly constructed phishing template.

Tracking / personalization tokens
Long numeric ID present (103882302891885308) and ID#2043 in subject — typical tracking or personalization tokens used by phishing campaigns.

Use of clickable unsubscribe / reply obfuscation
Truncated unsubscribe text and multiple sender headers (Sender, From, X-Google-Sender-Delegation) — attempt to look legitimate while hiding true origin.`  
  Concise list of observed phishing traits and recommended actions.
 
 ---

## Observed Phishing Traits (short)

- Display-name spoofing: uses `AAA_Emergency_Kit_Offer` while real sending domain is unrelated.
- Sender domain / Return-Path mismatch: `datastreamgalaxy.uk.net` and subdomains (random-looking).
- DMARC: **FAIL** (SPF & DKIM may pass, but DMARC fails — high risk).
- Message-ID inconsistency: references `convertkit-mail2.com`.
- Multipart email: plain + HTML — malicious links usually live in HTML part.
- Broken/placeholder content in body: `Sep 0, 2019`, long numeric token.
- Urgency/reward social engineering: subject promises a “Free Car Emergency Kit ⚡”.
- Likely mismatched URLs / trackers in HTML.

Risk: **High**

---

## How to safely inspect the email (step-by-step)

> ⚠️ Always perform these steps on an isolated machine or in a safe environment. Do NOT click links or open attachments.

1. Save the email as a `.eml` file from your mail client (File → Save as → `sample.eml`).
2. Open the `.eml` in a text editor (VS Code, Notepad++) — **do not** open embedded links by clicking.
3. Search the raw source for link attributes:
   - Search for `href="` and `src="` to list destinations.
4. Verify displayed link text vs `href` values:
   - If displayed text contains legitimate domain (e.g., `aaa.com`) but `href` points to another domain (e.g., `datastreamgalaxy.uk.net`), this is a mismatched (spoofed) URL.
5. Check authentication headers in the source:
   - `Received-SPF`, `DKIM-Signature`, `Authentication-Results`, `Return-Path`
   - Confirm DMARC alignment; a `DMARC: FAIL` is highly suspicious.
6. Extract all external domains for further lookup (WHOIS, reputation checks) on a safe device.

---
