# Joiner Workflow: Onboarding & Access Provisioning (Entra ID)

**Ironbridge Bank & Trust | MRA Finding #4 | Simulated enterprise environment**

---

## Video Walkthrough

**[Watch the 3 to 7 minute walkthrough](https://www.loom.com/share/00fc58c1c1514f41a47d2ef10fe057e0)**

---

## Problem Statement

Ironbridge Bank & Trust acquired Two Rivers Savings, and fourteen employees started on the same Monday. When I asked how onboarding had worked historically, the answer was four words: copy whatever Kevin has.

That practice produced two opposite failures. A part-time teller held wire transfer access for two years because nobody had granted it deliberately, they had inherited it through a copy. And a loan officer sat for nine days with no core banking access, unable to close loans, while payroll ran anyway.

The examiners required role-based onboarding with HR as the authoritative source, an approval workflow, and audit documentation for every access grant.

What struck me most about the two failures was that they come from the same gap: nobody ever defined what a role should have. Copying a person brings along all the access they've built up, including access nobody approved of. No copy = nothing gets granted. Over-access and under-access are both what happens when access is copied instead of decided.

---

## Solution Overview

I built role-based onboarding in Entra ID with HR as the authoritative source.

I established an HR roster as the single input for every account, then built a role catalog mapping each job title to exactly one role group. I created those groups in Entra and attached Microsoft 365 licensing to the groups rather than to individuals, so licensing is inherited through role membership and reclaimed automatically when membership ends.

I then provisioned all fourteen hires from the roster, placed each into a single role group, and verified that licensing, mailboxes and access flowed through membership. Finally I documented the justification for every grant and produced the audit evidence the finding required.

---

## Key Work

**Made HR the authoritative source.** Every account derives from the roster, not from an email or a manager's memory. When an examiner asks why a person holds an access, the answer predates the grant.

**Built a role catalog before provisioning anything.** Each job title maps to exactly one role. No title without a role, and no access decided in the moment.

**Attached licensing to groups, not people.** Membership carries the license, which means onboarding is one action instead of several and offboarding reclaims the license automatically.

**Scoped the wire operations hire deliberately.** His role group grants the operations desk and does not grant funds transfer access. That requires the system owner, a separation of duties review, and documented approval. IT does not grant it on request.

**Produced audit documentation for every grant.** Role membership exports, license inheritance evidence, and a written approval record tying each access back to a role definition.

---

## Tools Used

Microsoft Entra ID, Microsoft 365 admin center, Microsoft 365 Business Premium.

---

## Repository Contents

- `hr-roster.csv` - the authoritative source every account was built from
- `role-catalog.csv` - job title to role group mapping with license and scope
- `access-approval-record.md` - justification for every grant, and the wire exception
- `evidence/` - user export, role membership exports, license inheritance
- `screenshots/` - visual evidence across the onboarding workflow

---

## What I Learned

**Copying a coworker copies their history.**
The person you copy has been accumulating access for years, which means the new hire starts day one with the person's whole history: old projects. One-off exceptions, and rights nobody remembers granting. None of it was approved for them, and none of it can be justified for them.

**Licensing belongs on the role, not the person.**
A license attached to a group is inherited by every member and reclaimed when they leave it, which means offboarding reclaims the seat automatically instead of relying on someone to remember. No orphaned licenses on departed accounts, no paying for seats nobody uses, and the license count always matches who actually holds one.

**Day one readiness is a measurable cost.**
A hire who cannot work still gets paid, and every idle day costs the bank twice: salary for no output, and revenue that never comes in. Nine days without core banking access means nine dats of loans the bank did not close. Under-access does not trip an alarm the way over-access does, but just as costly.

**Order matters as much as accuracy.**
Seven of the fourteen hires report to someone else on the same roster, so a manager field won’t save until that manager’s account exists. Next time I’d sort the roster by reporting line before creating anything: branch managers first, then their tellers. A validation pass that checks dependencies, not just collisions and titles, turns a cleanup into a minute of planning.

---

*Built as part of the TotalThreat IT & IAM Career Accelerator. Ironbridge Bank & Trust is a simulated enterprise environment and not a real employer. The tenant configuration, role design, provisioning and documentation in this repository are my own work.*

