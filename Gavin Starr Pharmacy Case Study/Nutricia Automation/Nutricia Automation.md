---
type: implementation
client: "[[Gavin Starr Pharmacy Case Study]]"
status: discovery
created: 2026-11-10
tags: [implementation, sms, nutricia, textmagic]
---

# Nutricia Automation

## Problem
- 300+ Nutricia patients on repeat supply.
- Supply is tracked in a large Excel spreadsheet that shows when each patient needs a restock enquiry.
- Reminder texts are currently sent **by hand, one patient at a time**.

## Goal
Automatically text patients when they're due, then produce a report of who was messaged so an overseeing pharmacist can update the spreadsheet.

## Known facts
- The spreadsheet is an Excel file on a pharmacy PC, shared across all pharmacy computers.
- The sheet includes patient names, addresses and phone numbers.
- Patients have agreed to receive texts. Texting is currently manual.
- TextMagic is on the pharmacy's account. TextMagic has an MCP server.
- Message format: a fixed template that probably names the product (to be confirmed, see Q7).

## Unknowns
- How "due" is determined (a date column, or calculated?)
- Whether Fred or MedAdvisor already offers refill reminder SMS
- How patient replies are handled
- Whether sheet updates stay manual or are partly automated

## Design principles (draft)
- **Patient data never enters this vault.**
- Patient data should be processed by as few systems as possible. Preferred design: a script handles the matching and sending, so the AI never sees patient data. AI is used for reports with no names in them, triaging replies, and flagging data problems.
- A human pharmacist stays in the loop, either approving before send or reviewing after.
- Every send is logged (who and when, kept inside the pharmacy's systems only).

## Privacy and compliance notes
- Nutricia patient status implies a medical condition, so this counts as **health information** (sensitive information under the Privacy Act).
- TextMagic and AI tools are overseas services, so APP 8 (cross-border disclosure) applies. The owner needs to sign off and the privacy policy needs to cover it.
- Avoid putting the product name on lock-screen-visible texts unless the pharmacy approves.

## Questions sent to the pharmacy
### The spreadsheet
1. How do you decide when a patient is due for a reminder? Is there a "next due" date column, or do you work it out from the last supply date and how much they get?
2. Who updates the spreadsheet, and how often? Is it entered by hand or exported from Fred?
3. Is the sheet often left open on more than one computer at the same time?
4. Could you send me a copy of the sheet with only the column headers and 2–3 rows of fake data, no real patients?

### Fred
5. Has anyone checked whether Fred (or MedAdvisor, if you use it) already has a refill reminder SMS feature?

### The messages
6. What do you currently say in these texts? Please send me the exact wording you use most often.
7. Is it OK for the text to name the product? It will show on the patient's lock screen where others can see it. Or would you rather keep it general?
8. How many days before they run out should the reminder go out?
9. If a patient doesn't respond, do you send a second reminder? After how long?

### Replies
10. When patients reply now, what do they usually say?
11. Who should handle replies, and how should they see them: the TextMagic inbox, an email, or a daily list?
12. If someone replies STOP or says they've moved pharmacies, who updates the sheet?

### Reporting and checks
13. After the messages go out, what do you want to see: a list of who was texted, who replied, who's overdue?
14. Should a pharmacist approve the list before anything is sent, or is a report afterwards enough?
15. Would you be OK with the system marking "texted on [date]" in the sheet, with a pharmacist only checking it? Or should all updates stay manual?

### Privacy and ownership
16. Is the owner OK with patient names and numbers being processed by TextMagic and an AI tool (both overseas services)? Does the privacy policy cover this?
17. Which computer can the system run on each day? It needs to be one that's on during business hours.
18. Who's the contact if something goes wrong or a text goes out wrong?

**Most important:** Q1, Q4, Q5, Q16

## Answers
_Fill in as they come back._

## Decision log
| Date | Decision | Why |
|---|---|---|
| 2026-11-10 | Use Obsidian as the knowledge base, separate from Notion | Keeps client work separate and local |

## Status
- [x] Pitched and agreed (2026-11-10)
- [ ] Questions sent to the pharmacy
- [ ] Answers received
- [ ] Architecture decided
- [ ] Build
- [ ] Test with dummy data
- [ ] Pilot (small batch, pharmacist approval)
- [ ] Go live
- [ ] Write up the case study and extract a reusable framework
