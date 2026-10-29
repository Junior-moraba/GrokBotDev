---
type: use-case
slug: sa-matric-university-applications
headline: "South Africa: a matric learner's university, TVET and NSFAS deadline tracker"
summary: "A Grok Bot routine for South African matric learners and parents: it builds this year's university, CAO, TVET and NSFAS deadline calendar from official sites, works out the APS for each target programme, lists documents, and drafts applications without submitting them."
categories: [personal]
format: use-case
integrations:
  - Google Calendar
  - Gmail
  - Google Sheets
schedule: weekly
autonomy: acts-with-approval
difficulty: intermediate
setup_minutes: 30
cost_note: "NSFAS and many universities are free to apply; some charge a fee (e.g. Stellenbosch R100)"
author:
  handle: JMoraba22
  url: https://x.com/JMoraba22
  platform: x
prompt_provenance: author
replicability: "Works for any SA learner in Grade 11 or matric. Swap the institution list for your own. Dates are re-read from each official site every year, so nothing is hard-coded. Applications are made by the learner, not by the bot."
added_at: "2026-10-29T00:00:00Z"
updated_at: "2026-10-29T00:00:00Z"
status: proposed
---

## How it's set up

1. Tell the bot the learner's name, grade, subjects and latest marks (Grade 11 final or matric June/trial results), and 3-6 target programmes at universities or TVET colleges. Store the learner's ID number in the vault only.
2. Connect Google Sheets for a tracker (institution, programme, opening and closing dates, APS required vs learner's APS, fee, status) and Google Calendar for deadlines. Connect Gmail if application confirmations land there.
3. Paste the prompt below. On first run it builds the tracker from each institution's official site and the NSFAS site. Most selective programmes (medicine, health sciences, vet science) close as early as May-June, so start in Grade 11.
4. A weekly routine re-checks the official pages for changed dates, checks the tracker for missing documents, and reminds the learner 3 weeks, 1 week and 2 days before each deadline.
5. For each application the bot drafts answers and a document checklist. The learner logs in and submits on the official portal. Universities such as UJ explicitly refuse applications made by third parties.

## Prompt

```text
Role: University, TVET and NSFAS application coordinator for my child, a South African matric learner (Gauteng).

First run:
1. Ask for the learner's subjects and latest marks, the target programmes and institutions, and whether the household plans to apply for NSFAS.
2. Calculate the APS for each target. Convert each subject % to the NSC achievement level (1 = 0-29% ... 7 = 80-100%) and sum the best 6 subjects, normally excluding Life Orientation. Then apply each institution's own APS rules from its current prospectus (they differ, e.g. some count LO or weight Maths). Show the learner's APS next to the minimum per programme, and say clearly that meeting the minimum doesn't guarantee a place.
3. Build a Google Sheet tracker with institution, programme, application opening and closing dates, residence deadline, NBT requirement, application fee, APS required, learner's APS, documents, and status. Read every date and fee from the institution's official site, the CAO (cao.ac.za, for KZN institutions), the college's own site for TVET, or nsfas.org.za, and link the source page for each row. If a date can't be found on an official page, mark it "UNCONFIRMED". Never guess.
4. Flag any deadline that has already passed and any within 14 days in bold at the top.

Weekly routine (Mondays 07:00):
- Re-check the official pages for date changes and update the tracker. Tell me what changed.
- Remind us 3 weeks, 1 week and 2 days before each deadline (application, residence, NSFAS, NBT booking).
- List missing documents: certified ID copy, latest school report, proof of household income and parent/guardian IDs for NSFAS, consent forms.
- After results, remind us to upload final NSC results and track offers and acceptance deadlines.

Hard rules:
- Never submit an application, accept an offer, or pay an application fee without explicit go-ahead in this chat. The learner submits on the official portal themselves.
- Never put the learner's or parents' ID numbers in chat or files. Use the vault only, on the official form, while we watch.
- NSFAS is free to apply. Warn us about any site or person asking for money to "help" with NSFAS or university applications.
- Draft, don't decide: offer drafted motivational letters and form answers for the learner to edit.
```

## Why it's cool

South African application deadlines are scattered across dozens of sites, from May for medicine to the end of October for NSFAS and some universities, and each institution counts APS a little differently. One weekly routine that keeps a sourced tracker, does the APS maths per institution, and nags before every deadline gives a matric family the kind of help usually only well-resourced schools offer. The learner still clicks submit, so nothing is done in their name.

## Sources

Checked 29 Oct 2026 (SAST). These are the 2027-intake dates, as a sanity check. The bot re-reads them every year.

- NSFAS 2027 applications: opened 18 Sep 2026, close 31 Oct 2026, free to apply: https://nsfas.org.za/content/how-to-apply.html and https://www.gov.za/news/media-statements/nsfas-records-over-1-million-applications-2027-funding-cycle-board-joins
- UJ: closes 31 Oct 2026 at 12:00; free; two choices; APS excludes Life Orientation; no third-party applications (POPIA): https://www.uj.ac.za/admission-aid/undergraduate/important-information-before-you-apply/
- Wits: health sciences closed 30 Jun 2026; most programmes 30 Sep 2026: https://www.wits.ac.za/undergraduate/apply-to-wits/
- UP: opened 1 Apr 2026; vet science closed 31 May; others 30 Jun 2026: https://www.up.ac.za/online-application
- UCT: 1 Apr - 31 Jul 2026, no late applications: https://faculty.uct.ac.za/students/applications-apply-undergraduate-qualifications/application-procedure
- Stellenbosch: closed 31 Jul; up to 3 choices; R100 fee for SA applicants; NBT for some programmes: http://blogs.sun.ac.za/open-day/files/2026/03/How-to-Apply-Undergraduate-programmes-2027-intake.pdf
- UKZN via CAO; medicine closed 30 Jun 2026, others 30 Sep 2026: https://applications.ukzn.ac.za/2026-applications/ and https://www.cao.ac.za
- TVET: apply per college; DHET's 2027 window closed 30 Sep 2026: https://www.sanews.gov.za/south-africa/manamela-urges-youth-apply-early-tvet-colleges
- Not verified: the exact NSC %-to-level bands used above are the standard national scale but weren't re-checked against a DBE page this session. cao.ac.za shows 2027-entry material (handbook, FAQs); the CAO opening/closing dates and late fee must be read from the handbook, not assumed.
