# Kompas News Scraper and Email Reporter

This project is a Python script for scraping news articles from Kompas.com and sending daily reports via email. It utilizes various Python libraries for web scraping, email handling, and scheduling.

## Prerequisites

Ensure you have Python installed (version 3.6 or higher). You can install the required Python packages using the following command:

```bash
pip install -r requirements.txt
```

Alternatively, if using Pipenv, install the dependencies with:

```bash
pipenv install
```

Create a `requirements.txt` file with the following content:

```
beautifulsoup4==4.12.2
tqdm==4.66.1
pandas==2.1.1
apscheduler==3.10.2
pytz==2023.3
```

Or, create a `Pipfile` with the following content:

```
[[source]]
name = "pypi"s
url = "https://pypi.org/simple"
verify_ssl = true

[packages]
beautifulsoup4 = "*"
pandas = "*"
requests = "*"
apscheduler = "*"
email-validator = "*"
```

## How to Get Started

### Step 1: Configure Gmail SMTP Access

To send emails via Gmail, you need SMTP access. Follow these steps:

1. **Enable Two-Step Verification on your Google account:** Visit [Google Two-Step Verification](https://myaccount.google.com/security-checkup/2-step-verification) to enable it.

2. **Create an App Password:**
   - After enabling two-step verification, go to [Google App Passwords](https://myaccount.google.com/apppasswords).
   - Select the app (e.g., "Mail") and device (e.g., "Windows Computer") and click **Generate**.
   - Copy the generated 16-character password. This will be used as the password in the script.

### Step 2: Run the Script

Run the script using the terminal or command prompt:

```bash
python kompas_news_report.py
```

You will be prompted to enter several inputs:

- **Keyword:** The keyword for news search (e.g., "panda pink cafe").
- **From Email:** Your Gmail address (e.g., youremail@gmail.com).
- **To Email:** The recipient's email address. (e.g., dops@sonar.id)
- **Password:** The app password generated in Step 1.
- **Number of Pages to Scrape:** Number of pages to scrape from Kompas (e.g., 5).

### Step 3: Set Up the Scheduler (Optional)

The script includes a scheduler using APScheduler to run daily at 08:14 AM Jakarta time. If you wish to enable this feature, the script will automatically scrape news and send the report every day at the specified time.

To enable the scheduler, ensure the following lines are active:

```python
scheduler = BackgroundScheduler()
scheduler.add_job(main, 'cron', hour = 8, minute = 0, timezone='Asia/Jakarta')
scheduler.start()
```

If you want to run the script just once, comment out the scheduler section.

## Functions Overview

- **replace_indonesian_months(timestamp: str) -> str:** Converts Indonesian month names to English for datetime parsing.
- **Progress Class:** Manages the progress of data collection.
- **KompasConfig Class:** Stores configuration for Kompas scraping.
- **read_page_kompas(url: str) -> List[str]:** Reads a page from Kompas and extracts news article links.
- **get_multi_pages_kompas(config: KompasConfig) -> List[str]:** Retrieves links from multiple pages.
- **get_news_content_kompas(url: str):** Extracts content details from a news article.
- **send_email(report_df: pd.DataFrame, ...):** Sends the news report via email.
- **main():** Main function that orchestrates scraping, report generation, and sending the email.

## Security Note

Using your Gmail credentials in the script requires caution. Make sure you do not share your app password and avoid uploading it to public repositories.

## Example Usage

Run the script in your terminal:

```bash
python kompas_news_report.py
```

Provide the required inputs as prompted, and the script will scrape news articles from Kompas and send a report to the specified email address.

## Scheduler Feature

The script can automatically run daily using APScheduler. This feature can be useful if you want to receive daily news updates without manual intervention.

To enable the scheduler, ensure the following lines are active:

```python
scheduler = BackgroundScheduler()
scheduler.add_job(main, 'cron', hour = 8, minute = 0, timezone='Asia/Jakarta')
scheduler.start() 
```

This will trigger the `main()` function every day at 08:00 AM Jakarta time.

## License

This project was created by Muhammad Dhoni Apriyadi and is open-source, available for modification or distribution under the MIT License.

## Acknowledgments

This script uses data from Kompas.com. Special thanks to the Python community for providing amazing libraries to make tasks like web scraping and email automation simpler.
