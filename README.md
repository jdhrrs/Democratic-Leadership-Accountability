# Congressional Accountability Email Scripts Version 1.0

Automated Google Apps Script tools designed to send scheduled, rotating advocacy messages to U.S. Senate and U.S. House of Representatives offices on an hourly basis.

## Overview

This repository contains two standalone Google Apps Script projects:
* **Senate Accountability Script:** Sends hourly top-of-the-hour (`:00`) email batches to Senate communications directors and press offices.
* **House Accountability Script:** Sends hourly top-of-the-hour (`:00`) email batches to House of Representatives offices.

Both scripts automatically rotate through an array of subject lines and message bodies so recipients receive varied communications across scheduled batches, and both include built-in daily caps to stay within Gmail's sending limits.

---

## Features

* **Top-of-the-Hour Scheduling:** Automatically locks triggers to the exact `:00` mark of each hour (`America/Chicago` timezone by default).
* **Full-List Hourly Batches:** Sends an email to every recipient in the `RECIPIENT` array during each hourly run.
* **Dynamic Content Rotation:** Cycles through `SUBJECT` and `MESSAGE` arrays across recipients and hours so consecutive emails are not identical.
* **Automatic Quota Protection:** Tracks total emails sent via `PropertiesService` and automatically deletes active triggers once `MAX_EMAILS` is reached.
* **Built-in Controls:** Includes helper functions to start, stop, and check the real-time status of a campaign.

---

## Setup Instructions

Because Google Apps Script projects run independently on Google's cloud servers, set up each script in its own project:

1. Open [Google Apps Script](https://script.google.com/) and create a **New Project** (e.g., *Senate Accountability* or *House Accountability*).
2. Delete any placeholder code in `Code.gs` and paste the contents of the respective script file.
3. Click **Save** (`Ctrl + S` / `Cmd + S`).
4. Select `startCampaigN` from the function dropdown menu at the top and click **Run**.
5. Grant the required Gmail and trigger permissions when prompted.

---

## Usage & Controls

Manage either script directly from the function dropdown menu in the Google Apps Script editor:

| Function | Description |
| :--- | :--- |
| `startCampaigN()` | Resets the counter to `0`, sends the first batch immediately, and schedules subsequent batches for the top of every hour (`:00`). |
| `stopCampaigN()` | Immediately deletes all active time-based triggers and halts the campaign. |
| `checkStatus()` | Logs the current progress (`Total Emails Sent: X / MAX_EMAILS`) in the **Executions** log. |

> **Tip:** To wait until the next `:00` mark before sending the first batch instead of sending immediately on start, replace `sendHourlyEmaiL();` with `scheduleNextTopOfHour();` inside `startCampaigN()`.

---

## Configuration & Gmail Limits

At the top of both scripts, you can adjust the following constants:

* `TIMEZONE`: Set to `"America/Chicago"` by default.
* `RECIPIENT`: Array of target email addresses (e.g., 48 Senate contacts in the Senate script).
* `SUBJECT` & `MESSAGE`: Arrays of rotating email subjects and body templates.
* `MAX_EMAILS`: Total number of emails sent before the script automatically shuts itself off.

### Gmail Daily Sending Quotas
* **Standard `@gmail.com` accounts:** Limited to **500 emails** per rolling 24-hour period. Keep `MAX_EMAILS` at or below `480` per 24 hours to prevent temporary account locks.
* **Google Workspace accounts:** Limited to **2,000 emails** per rolling 24-hour period. If running both the Senate and House scripts simultaneously from separate accounts, track each account's daily quota independently.

---

## Responsible Use

This software is intended solely for lawful civic engagement, public advocacy, and constituent communication. By downloading, configuring, or running these scripts, you agree to:

* **Comply with Platform Policies:** Adhere strictly to [Google's Terms of Service](https://policies.google.com/terms), [Gmail Program Policies](https://www.google.com/gmail/about/policy/), and all applicable daily sending limits.
* **Avoid Harassment or Abuse:** Never use these scripts to send threatening, defamatory, deceptive, fraudulent, or malicious communications, nor to conduct denial-of-service or spam attacks against public or private infrastructure.
* **Verify Recipient Lists & Content:** Take full responsibility for reviewing and maintaining accurate recipient addresses and message templates prior to execution.
* **Follow Applicable Laws:** Ensure your use complies with all local, state, and federal laws and regulations governing electronic communications.

---

## Disclaimer & Release of Liability

**AS-IS SOFTWARE:** These scripts and accompanying documentation are provided **"AS IS"**, without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, or non-infringement.

**RELEASE OF LIABILITY:** In no event shall the author(s), contributor(s), or distributor(s) of this repository be held liable for any direct, indirect, incidental, special, exemplary, or consequential damages—including, without limitation, suspended or terminated Google/Gmail accounts, blocked email delivery, loss of data, reputational harm, or legal claims—arising out of or in any way connected with the use, misuse, or inability to use these scripts. You assume full and sole responsibility for all actions taken and communications sent using this software.
