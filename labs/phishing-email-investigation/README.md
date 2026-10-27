# Lab 02 Phishing Email Investigation

**Author:** Victoria Wanja  
**Completed:** October 27, 2026  
**Format:** Guided SOC analyst tabletop exercise with AI feedback

In this fictional exercise, I investigated a payroll phishing email, assessed a simulated account compromise, and developed a containment plan. The scenario progressed from a suspicious message to credential theft, unauthorized email forwarding, and a payroll file download.

## Scenario and email evidence

All addresses, messages, and events below are invented training material. The `.example` domains are placeholders. This was a discussion exercise; I did not inspect a live mailbox or operate incident response tools.

The company's official email domain was `company.example`.

```text
From: Payroll Support <payroll@company-payroll.example>
To: victoria@company.example
Subject: URGENT: Your salary payment is on hold

Hello Employee,

Your salary cannot be processed until you verify your
Microsoft account within 30 minutes.

Verify here:
https://company-payroll.example/verify

Enter your work email, password, and verification code
to prevent a payment delay.

Payroll Department
```

## Analysis

| Evidence | Assessment |
| --- | --- |
| Sender uses company-payroll.example | The domain differs from company.example and imitates a payroll service. The repeated word “payroll” alone is not proof of phishing. |
| Recipient uses company.example | This identifies the intended employee; a legitimate recipient address does not authenticate the sender. |
| Request for a password and verification code | Supplying both could enable an attacker to complete a sign-in. |
| Threat of a salary delay within 30 minutes | Financial pressure and urgency encourage action before verification. |
| Verification link uses the sender's different domain | The link is part of the suspicious credential request and should not be followed. |

My initial advice was not to reply. The discussion expanded that advice to avoiding the link, reporting the message through the company's process, and confirming payroll questions through a known internal contact.

## Simulated investigation

The employee initially reported clicking without entering information, then disclosed entering both their work password and verification code. That disclosure changed the response from investigating a click to treating the account as potentially compromised.

The scenario introduced an unfamiliar successful sign-in two minutes after credential submission, followed by an external forwarding rule and a file download:

```text
10:02  Suspicious successful login
10:04  External forwarding rule created
10:06  Payroll.xlsx downloaded
```

The unfamiliar IP and timing were strong grounds for immediate action, although an unfamiliar IP alone does not establish who signed in. Device details, session activity, and employee confirmation would help validate the assessment.

The rule forwarded all incoming email to an unknown external address, creating a risk of ongoing email disclosure. The payroll download indicated suspected exposure of payroll data; its contents and sensitivity would need investigation.

## Proposed response

These are response actions discussed in the exercise, not actions performed on a real account.

1. Escalate through the organization's incident response process.
2. Revoke active sessions and reset the compromised password promptly.
3. Preserve the forwarding rule's details and disable the unauthorized rule.
4. Review sign-in and audit logs to establish the access window and affected emails or files.
5. Check for unauthorized MFA changes and other account settings that could preserve access.
6. Assess the contents of Payroll.xlsx and coordinate the response to possible sensitive data exposure.

Removing the forwarding rule does not terminate an active session. A password reset alone may also leave existing sessions active.

## My reasoning and learning

During the discussion, I recognized that stolen credentials could expose sensitive information, identified urgency as a way to make the message seem serious, and called for immediate investigation of a possible active attacker session. I also recommended disabling the forwarding rule and identified the payroll document as potentially compromised.

Feedback helped me distinguish clicking a link from entering credentials, separate containment actions from investigation, and avoid treating a suspicious IP as conclusive attribution.

I suggested stronger passwords, employee vigilance, and biometrics. The discussion clarified that a strong password can still be phished, and that the protection provided by biometrics depends on the authentication system in which they are used.

## Final incident summary

An attacker impersonated payroll in a phishing email. An employee followed the link and entered their work password and verification code. In the fictional scenario, the attacker accessed the account, created an unauthorized external forwarding rule, and downloaded Payroll.xlsx, creating suspected exposure of payroll data.

The proposed response was to revoke active sessions, reset the password, disable the forwarding rule, and review audit logs to determine the extent of access.

## Skills practiced

- Recognizing phishing indicators and social engineering.
- Asking follow-up questions about credential exposure.
- Assessing suspicious authentication activity.
- Planning account containment and evidence preservation.
- Interpreting email forwarding and file download events.
- Writing an incident summary.

This project records guided learning with AI-generated scenario evidence and feedback. It does not represent professional incident response experience.
