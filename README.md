# Victoria Wanja Cybersecurity Portfolio

This portfolio documents my cybersecurity learning through practical labs, evidence, and investigation reports. My current focus is authentication logs, SIEM dashboards, phishing analysis, and explaining security findings clearly.

## Projects

### Investigating repeated failed logins with Kibana

In this guided personal lab, I used Kibana to explore simulated login activity and connect an account, source IP, and burst of failed logins. The dataset contains 680 invented authentication events. An investigation isolated 80 failed attempts against `alex` from one source, two seconds apart.

[Read the investigation and view the dashboard](labs/kibana-login-investigation/README.md)

![Kibana login security dashboard](labs/kibana-login-investigation/screenshots/dashboard.jpg)

### Lab 02 Phishing email investigation

In this guided tabletop exercise, I examined a fictional payroll phishing email and worked through credential theft, an unauthorized forwarding rule, and a payroll file download. I practiced assessing evidence, proposing containment, and writing an incident summary.

[Read the phishing investigation](labs/phishing-email-investigation/README.md)

## Skills practiced

- Searching authentication logs with Kibana Query Language (KQL).
- Comparing failed logins by account, time, and source IP.
- Distinguishing suspicious activity from evidence of successful compromise.
- Documenting findings and preserving dashboard exports.
- Recognizing phishing indicators and social engineering.
- Planning account containment and assessing possible data exposure.

## Learning context

These are educational projects using simulated data. The Kibana lab was completed with AI guidance for setup, queries, dashboard construction, and documentation. The phishing lab was a discussion exercise with AI-generated evidence and feedback. These projects represent guided learning rather than professional incident response experience.
