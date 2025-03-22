git clone https://github.com/your-username/dynamic-calendar.git

from icalendar import Calendar, Event
from datetime import datetime, timedelta
import pytz

# Set timezone for events
timezone = pytz.timezone("America/New_York")

# sis Invitational", "location": "Pacific Palisades, CA", "start": datetime(2025, 2, 13), "end": datetime(2025, 2, 16)},
    {"summary": "The Honda Classic", "location": "Palm Beach Gardens, FL", "start": datetime(2025, 2, 20), "end": datetime(2025, 2, 23)},
    {"summary": "Arnold Palmer Invitational", "location": "Orlando, FL", "start": datetime(2025, 3, 6), "end": datetime(2025, 3, 9)},
    {"summary": "THE PLAYERS Championship", "location": "Ponte Vedra Beach, FL", "start": datetime(2025, 3, 13), "end": datetime(2025, 3, 16)},
    {"summary": "Valero Texas Open", "location": "San Antonio, TX", "start": datetime(2025, 3, 27), "end": datetime(2025, 3, 30)},
    {"summary": "Masters Tournament", "location": "Augusta, GA", "start": datetime(2025, 4, 10), "end": datetime(2025, 4, 13)},
    {"summary": "RBC Heritage", "location": "Hilton Head, SC", "start": datetime(2025, 4, 17), "end": datetime(2025, 4, 20)},
    {"summary": "Wells Fargo Championship", "location": "Charlotte, NC", "start": datetime(2025, 5, 1), "end": datetime(2025, 5, 4)},
    {"summary": "PGA Championship", "location": "Charlotte, NC", "start": datetime(2025, 5, 15), "end": datetime(2025, 5, 18)},
    {"summary": "U.S. Open", "location": "Pinehurst, NC", "start": datetime(2025, 6, 12), "end": datetime(2025, 6, 15)},
    {"summary": "The Open Championship", "location": "St. Andrews, Scotland", "start": datetime(2025, 7, 17), "end": datetime(2025, 7, 20)}
]

# Generate the calendar file
cal = Calendar()
cal.add('prodid', '-//Dynamic Calendar Generator//EN')
cal.add('version', '2.0')

for event_data in events:
    event = Event()
    event.add('summary', event_data['summary'])
    event.add('location', event_data['location'])
    event.add('dtstart', timezone.localize(event_data['start']))
    event.add('dtend', timezone.localize(event_data['end']))
    event.add('dtstamp', datetime.now(timezone))
    cal.add_component(event)

# Save the file locally
ics_filename = "dynamic_schedule.ics"
with open(ics_filename, 'wb') as f:
    f.write(cal.to_ical())

print(f"ICS file '{ics_filename}' generated successfully.")

# Instructions for Hosting and Automation
instructions = """
1. **Host the .ics file:**
   - Upload `dynamic_schedule.ics` to a public GitHub repository and enable GitHub Pages.
   - Alternatively, use AWS S3, Netlify, or another hosting platform.

2. **Automate Updates:**
   - Use a cron job or GitHub Actions to run this script periodically.
   - Example cron job (runs daily):
     ```
     0 0 * * * /path/to/python3 /path/to/this_script.py
     ```

3. **Subscribe to the Calendar:**
   - Copy the public URL of the `.ics` file and subscribe via your calendar app.
     - **Google Calendar:** Go to "Other calendars > Add by URL" and paste the link.
     - **Apple Calendar:** File > New Calendar Subscription.
     - **Outlook:** Add calendar > Subscribe via URL.

"""

print(instructions)


git add .
git commit -m "Add initial calendar file"
git push origin main

