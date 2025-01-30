# Dynamic-iCalendar
git clone https://github.com/your-username/dynamic-calendar.git
from icalendar import Calendar, Event
from datetime import datetime, timedelta
import pytz
import os

# Set timezone for events
timezone = pytz.timezone("America/New_York")

# Sample dynamic events (in a real setup, these might come from an API or database)
events = [
    {"summary": "Team Meeting", "location": "Zoom", "start": datetime.now() + timedelta(days=1), "end": datetime.now() + timedelta(days=1, hours=1)},
    {"summary": "Project Deadline", "location": "Online", "start": datetime.now() + timedelta(days=5), "end": datetime.now() + timedelta(days=5, hours=2)},
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
