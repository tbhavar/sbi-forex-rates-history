# 💹 Daily SBI Forex Rate Scraper

## 🚀 Project Overview

This repository uses **GitHub Actions** to automatically scrape and archive the daily State Bank of India (SBI) Forex Card Rates PDF.

The primary goal is to maintain a reliable, historical record of the official exchange rates by ensuring a copy of the rates PDF is downloaded and committed to this repository every day.

The rates are scraped from the official SBI website document link.

---

## 💾 Repository Structure

The scraped PDFs are stored in a clear, year-based hierarchy:

---

## ⚙️ Automation Details (GitHub Actions)

This repository uses a single GitHub Actions workflow to handle the scraping, committing, and failure notification.

### ⏰ Schedule

The workflow is automatically triggered daily via a `cron` schedule.

| Trigger Event | Time (UTC) | Time (IST / GMT+5:30) |
| :--- | :--- | :--- |
| **`schedule`** | `30 9 * * *` | **3:00 PM** |

### 🔑 Key Workflow Steps

1.  **Download & Fortify:** A `curl` command downloads the PDF. It uses a randomized **User-Agent** and essential **Referer** and **Accept-Language** headers to successfully appear as a legitimate browser request, preventing common server-side blocking that results in small error files.
2.  **Validation:** The script checks that the downloaded file size is greater than **1000 bytes** to ensure a valid PDF was retrieved instead of a small HTML error page.
3.  **Commit:** If successful, the new PDF is added to the `sbi-tt-rates-historical` folder and committed back to the repository.
4.  **Notification:** If the scraping or committing fails, a separate job runs to send an email notification (requires the `MAIL_PASSWORD` secret to be set).

---

## 🧑‍💻 Manual Execution

To manually run the scraper (e.g., for testing or immediate updates):

1.  Go to the **Actions** tab of this repository. 
2.  Click on the **`Daily SBI Rate Scraper`** workflow in the left sidebar.
3.  Click the **"Run workflow"** dropdown button on the right side.
4.  Click **"Run workflow"** to start the job.

---

## 📧 Failure Notifications

The workflow is set up to send a notification email upon failure. This requires the following secret to be configured in your repository's settings:

| Secret Name | Description |
| :--- | :--- |
| `MAIL_PASSWORD` | The **App Password** for the Gmail account (`catanmaybhavar@gmail.com`) used to send the failure notifications. |
