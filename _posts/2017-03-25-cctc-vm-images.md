---
title: "CCTC Challenge VM"
tags:
 - cctc
 - india
 - vm
 - security
 - ctf
 - pentesting
layout: post
---

This is specifically about the contest held in 2011,
6 years ago. I've written about my experience
during the contest [on this blog](/blog/2011/11/20/cctc-blog/).

More specifically, Round 2 of the contest was a pentesting
scenario where we were only provided with a VM image
and asked to test it and report any vulnerabilities
that we found.

I recently found the VirtualBox images, and thought
I'd share them as a easy intro to web security.


# Instructions

1. [Reach out to me](/contact/) for the VM image
2. Hack.
3. Credentials are student:student (username:password)
4. Open <VM_IP>/cctc in your browser.

# Rules
1. Only application and its serving components can be tested for vulnerabilities. The serving components include
  - Webserver
  - Operating System
  - Any other services/files in the guest machine and guest operating system
2. Any vulnerability identified in any component outside the above mentioned ones, will not be used for evaluation
3. All participants should necessarily submit all the exploit codes/custom scripts written to identify the vulnerabilities in the system.
4. The deadline for the original challenge was 2 weeks, but you're free to take as much time as you want. Feel free to publish a list of vulnerabilities you find.

[The attached spreadsheet][spreadsheet] provides format of the report, challenges in scope, and the details to be filled out for each vulnerability identified.

The tasks to be performed are mentioned in the report. Each task consists of the following sections:

1. Vulnerability/Vulnerabilities - You need to write the description of the vulnerability
2. Root Cause(s) - What is the root cause of the vulnerability?
3. Approach adopted (Steps with screenshots) – Write the steps followed to exploit the vulnerability along with screenshot of the final screen and/or intermediate steps.
4. Remediation with sample code snippet – Write the remediation steps to address this vulnerability. Also, write the sample code if applicable.

Also [attached is a step by step installation guide][setup] for application set-up.

Few points to be considered:

- Challenges can be attempted and completed in any order.
- Only the application and its serving components can be tested for vulnerabilities. All other components like VMware, if tested for security issues, would lead to disqualification.
- I will not be responsible for the discovery/notification of any zero day vulnerability in any software.  If any zero-day vulnerability is identified, it is the responsibility of the concerned participant to notify the vulnerability to the respective vendor as per vendor’s policy.

If you are really interested, you can find a copy of the report
we submitted at [/reports/cctc](/reports/cctc/).

Thanks to Harshil and Shobhit for working alongside on this.

[spreadsheet]: https://docs.google.com/spreadsheets/d/1s_o-HGlS2dKbDnm2mjTbgXpDHDHQgMYXlbOMEVNaBvY/edit?usp=sharing
[setup]: https://drive.google.com/file/d/0B2qzfUR1eWklMHJONkZPUkVqLWZPS3pwTzFDYW84aVJhbjZB/view?usp=sharing