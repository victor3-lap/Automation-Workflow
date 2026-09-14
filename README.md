# Job Application Tracker (n8n Workflow)

An n8n automation that handles the full lifecycle of a job application — from form
submission to candidate communication — with experience-level routing.

## What it does

1. **Application form** — A public form collects: Full Name, Email, Phone Number,
   Applying Position (dropdown), Years of Experience (dropdown), Current Location,
   and a CV/portfolio link.
2. **Application Database** — Each submission is appended as a row to a Google Sheet.
3. **Confirmation Mail** — The candidate immediately receives an email confirming
   their application was received.
4. **HR Email** — The HR inbox is notified of the new application with the
   candidate's details.
5. **Experience routing (Switch)** — Applications are tagged as Entry Level (0–2 yrs),
   Mid Level (3–5 yrs), or Senior Level (6+ yrs).
6. **Decision branch (If)** — A simple pass/fail check on experience level determines
   the next email:
   - **Ejection mail** — sent after a 2-day wait if the candidate doesn't meet
     the experience bar.
   - **Interview mail** — sent after a 2-day wait, inviting the candidate to
     interview, if they do meet the bar.

## Nodes used

| Node | Type |
|---|---|
| Application form | `formTrigger` |
| Application Database | `googleSheets` |
| Confirmation Mail / HR Email / Ejection mail / Interview mail | `gmail` |
| If | `if` |
| Switch | `switch` |
| Wait / Wait1 | `wait` (2 days) |

## Setup

1. Import `Job_Application_Tracker.json` into your n8n instance
   (**Workflows → Import from File**).
2. Reconnect credentials — this export does **not** include OAuth secrets:
   - Google Sheets OAuth2 (for the Application Database node)
   - Gmail OAuth2 (for the four email nodes)
3. Replace `YOUR_GOOGLE_SHEET_ID_HERE` in the Application Database node with the
   ID of your own Google Sheet.
4. Update `hr-team@example.com` in the HR Email node to your actual HR inbox.
5. Adjust the email copy (currently branded "Okafor Logistics") to your company name.
6. Activate the workflow and grab the form's public URL from the
   Application form trigger node.

## Notes

- The experience-level logic is a placeholder — you may want to replace the simple
  0–2 / 3–5 / 6+ cutoff with something more nuanced (e.g. per-role thresholds).
- The 2-day wait before sending accept/reject emails is intentional (gives HR a
  window to intervene manually) but can be shortened or removed.
