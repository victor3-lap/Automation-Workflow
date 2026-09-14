# n8n Workflows

A collection of n8n automation workflows.

---

## 1. Job Application Tracker
**File:** `Job_Application_Tracker.json`

Handles job applications end-to-end: a public form collects candidate details,
logs them to Google Sheets, sends a confirmation + HR alert, then routes to
either an interview invite or rejection email based on years of experience
(2-day wait before that final email).

**Setup:**
- Reconnect Google Sheets OAuth2 + Gmail OAuth2.
- Replace `YOUR_GOOGLE_SHEET_ID_HERE` in the Application Database node.
- Replace `hr-team@example.com` with your real HR inbox.
- Update "Okafor Logistics" branding in email copy to your company name.

---

## 2. Lead Management
**File:** `Lead_Management.json`

Captures leads from a website quote form, logs them to Google Sheets, sends
the lead a welcome email, and alerts the sales team via Slack + email.

**Setup:**
- Reconnect Google Sheets OAuth2 + Gmail OAuth2 + Slack OAuth2.
- Replace `YOUR_GOOGLE_SHEET_ID_HERE` in the Leads Database node.
- Replace `sales-team@example.com` with your real sales inbox.
- Repoint the Slack node from `slackbot` to your team's actual channel.
- Update "B&B" branding in the welcome email.

---

## 3. Weather Telegram Bot
**File:** `Weather_Telegram_Bot.json`

Sends a daily 6am weather report for Lagos to a Telegram chat. Includes an
unused Telegram Trigger node (not wired in — possibly for a future
on-demand feature).

**Setup:**
- Reconnect OpenWeatherMap API + Telegram API credentials.
- Replace `YOUR_TELEGRAM_CHAT_ID_HERE` with your own chat ID.
- Change `cityName` if you want a different city.

---

## 4. Event Registration
**File:** `Event_Registration.json`

Polls a Google Form response sheet for new event registrations, sends a
session-specific confirmation (Blockchain / Career Talk / Health), then a
reminder email closer to the event date.

**Setup:**
- Reconnect Google Sheets Trigger OAuth2 + Gmail OAuth2.
- Replace `YOUR_GOOGLE_SHEET_ID_HERE` in the Google Sheets Trigger node.
- Update the hardcoded `Wait` dates and "December 15th" event date in the
  reminder copy.
- **Known bug:** the first "Send a message" reminder node sends to the
  registrant's Full Name instead of Email — fix it to reference `Email`
  like the other two reminder nodes do.

---

## General notes

- None of these exports include actual OAuth tokens/API keys — only
  credential *names/IDs*. You'll need to reconnect each credential in your
  own n8n instance after importing.
- Google Sheet IDs, personal emails, and chat IDs have been replaced with
  placeholders — swap in your own before activating.
