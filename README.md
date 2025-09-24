# Phishing Email Analysis

## 📌 Objective
The goal of this task is to analyze a suspicious email and identify phishing characterstics such as spoofed sender details,  fake links,  and social engineering tactics.

---

## 📧 Sample Email Quick Summary
- **From:** `Support <support@msupdate.net>`  
- **Subject:** Microsoft account password change  
- **Headline:** Your password changed  
- **Account mentioned:** `ethan@hooksecurity.co`  
- **Security info shown:** Country/region: United States · Platform: iOS · Browser: Safari · IP address: `77.196.86.10`  
- **Action links visible:** Reset your password · Review your security info · Learn how to make your account more secure · opt out  
- **Signature:** The Microsoft account team

---

## 🔍 Analysis
**Sending domain mismatch**  
   - Email comes from `msupdate.net`. Official Microsoft security emails normally come from `microsoft.com`, `account.microsoft.com`, `microsoftonline.com`, or other   Microsoft-owned domains. `msupdate.net` is not an official Microsoft domain → **suspicious**.

   **Brand impersonation**  
   - Styling and wording mimic Microsoft to build trust. Attackers commonly copy legitimate branding and then use a non-Microsoft sending domain.

   **Action links likely spoofed**  
   - Although link text looks legitimate, attackers often set the displayed text to a trusted URL while the actual href points elsewhere. Do **not** click; hover to inspect actual URLs or copy them (without opening) and scan.

    **Social-engineering pressure / plausible content**  
   - The email notifies about a password change and provides steps to recover — a common phishing lure to get users to click and enter credentials.

   **Inclusion of IP & location**  
   - Listing an IP and location can increase perceived legitimacy. This can be faked or taken from a third-party; it is not by itself proof of legitimacy.

    **No raw headers shown**  
   - The screenshot does not include authentication headers (SPF / DKIM / DMARC). Without raw headers, we cannot confirm whether mail authentication passed.
**Preliminary verdict:** **Highly suspicious / likely phishing**. Final confirmation requires header analysis and safe URL/WHOIS checks.

---

## ⚠️ Immediate recommended actions (for the recipient)
**Do NOT click any link** in this email.  
- Open a browser and go directly to `https://account.microsoft.com` (type it yourself) to check recent sign-in activity.  
- If you suspect compromise: change your Microsoft password from the official site and enable MFA.  
- Report the message to Microsoft (for Office365: `phish@office365.microsoft.com`) or use your email provider’s “Report phishing” function.  
- If you accidentally entered credentials, change the password immediately and review other accounts that used the same password.


---

## ✅ Technical Verification steps (what to collect and check safety)
**Save the raw headers** (`headers.txt`)  
   - In Gmail: *Show original* → copy raw headers.  
   - Check `Authentication-Results:` for **SPF / DKIM / DMARC** (pass / fail). Note and explain results in `headers_analysis.md`.

**Inspect Received chain** (from bottom → top)  
   - Find origin IP in the bottom-most `Received:` line. Compare origin host/IP to Microsoft’s known mail servers. Document findings in `headers_analysis.md`.

**Extract and check actual URLs** (do not open them)  
   - Hover to reveal hrefs or copy link targets as plain text. Scan those URLs on VirusTotal / URLhaus and save results as `url-analysis.md` and screenshots in `screenshots/`.

**WHOIS lookups**  
   - WHOIS for `msupdate.net` → save as `whois_msupdate_net.txt`.  
   - WHOIS / IP lookup for `77.196.86.10` → save as `whois_ip_77.196.86.10.txt`. Note registrar, creation date, and whether domain/IP belong to known Microsoft infrastructure.

**Reverse DNS / Mail server checks**  
   - Check whether the sending IP resolves to a Microsoft mail server or to a third-party hosting provider (document results).

**Archive evidence**  
   - Save screenshots: email body, header analyzer output, URL scan results. Place under `screenshots/`.

   ---

##  📝 Suggested Short Conclusion 
 **Verdict:** Likely phishing. The sending domain (`msupdate.net`) does not match Microsoft official domains; the message uses Microsoft branding and urges action via links. Without raw header authentication results, final confirmation is pending, but do not interact with the links — verify via the official Microsoft site.  

