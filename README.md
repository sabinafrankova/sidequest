# Sidequest

Hobby classes for every level in Montréal, taught by students and local hobbyists. First class free, then pay per class.
Group 6 project for INSY 440 E-Business, McGill, Fall 2026.

The whole site is one file, `index.html` (HTML, CSS and JavaScript together), so it can be opened directly,
hosted on GitHub Pages, or pasted into a Wix **Embed code** element.

## What's in the repo

| File | What it is |
|---|---|
| `index.html` | The whole site: every page, style and script |
| `404.html` | The "This quest doesn't exist" page GitHub Pages shows for addresses that don't exist |
| `email/confirmation-template.html` | The booking confirmation email, to paste into EmailJS |
| `email/notice-template.html` | Optional second email for reminders and teacher notices |
| `images/` | The class photos (add them yourselves, see below) |
| `README.md` | This file |

## Run it

Open `index.html` in a browser. No build step and no installs.

## Put it online with GitHub Pages

1. Push this repo to GitHub (on a free account the repo must be public for Pages).
2. Go to **Settings → Pages**, set the source to **Deploy from a branch**, branch `main`, folder `/ (root)`.
3. After a minute the site is live at `https://<your-username>.github.io/<repo-name>/`.

## Switch on confirmation emails (EmailJS)

The site sends the confirmation through [EmailJS](https://www.emailjs.com), which works from a static site with no server.
The free plan covers 200 emails a month.

1. Create a free EmailJS account.
2. **Email Services → Add New Service**: connect the team Gmail (or Outlook). Copy the **Service ID**.
3. **Email Templates → Create New Template**:
   - Subject: `You're booked: {{class_title}} on {{class_date}}`
   - To Email: `{{email}}`
   - From Name: `Sidequest`
   - Reply To: the team email
   - Content: open the code editor and paste everything from `email/confirmation-template.html`.
   - Save, then copy the **Template ID**.
4. **Account → General**: copy the **Public Key**.
5. In `index.html`, find `const EMAIL = {` and replace the `YOUR_...` values. Commit and push.
6. Optional, for reminders and teacher notices: create a second template with Subject `{{subject}}`, To Email `{{email}}`,
   and the content of `email/notice-template.html`. Put its ID in `noticeTemplateId`. The free plan allows 2 templates, so this uses both.

How it behaves:
- While the three values are still `YOUR_...`, the confirmation page says emails aren't switched on and shows every detail on screen.
- If sending fails (no connection, wrong ID, monthly limit reached), the page says so, keeps the booking, shows every detail and offers **Try again**. This is the unhappy path from story 2.3.
- The claude.ai preview of the site blocks outside connections, so emails only go out from GitHub Pages (or Wix).

Because the recipient comes from the form, anyone who opens the page can trigger an email to an address they type.
That's fine for a class demo; for real use, add reCAPTCHA in EmailJS or send emails from a server.

## Photos

Every class shows a photo from the `images/` folder. Until a file is there, the site shows a colour block with the hobby name instead.
Use your own photos (best: the team actually teaching) or free ones from Unsplash or Pexels. Landscape or square, about 1200px wide, JPG.

| File | What it should show |
|---|---|
| `pottery-banner.jpg` | Someone shaping clay at a pottery wheel (wide photo, used on the home page) |
| `dance.jpg` | A small group learning a hip-hop routine |
| `dance-advanced.jpg` | A contemporary dancer mid-move |
| `guitar.jpg` | Hands playing chords on an acoustic guitar |
| `guitar-advanced.jpg` | Close-up of fingers picking guitar strings |
| `tennis.jpg` | A player hitting a forehand |
| `badminton.jpg` | A badminton player going for a smash |
| `pottery.jpg` | Hands shaping a small clay cup |
| `pottery-wheel.jpg` | Hands centring clay on a pottery wheel |
| `photography.jpg` | Someone taking a photo with their phone in the street |
| `drawing.jpg` | A charcoal figure drawing |
| `sewing.jpg` | Fabric going through a sewing machine |
| `pilates.jpg` | A small group doing Pilates on mats |
| `ice-skating.jpg` | Skaters on an outdoor rink |
| `terrarium.jpg` | A small glass terrarium with moss |
| `yoga.jpg` | A small group holding a yoga pose |
| `piano.jpg` | Hands on piano keys |
| `singing.jpg` | A small group singing around a piano |
| `climbing.jpg` | A climber on a bouldering wall |
| `running.jpg` | A small group running in a park |
| `painting.jpg` | A watercolour painting in progress |

Newer classes in an existing hobby reuse that hobby's photo (for example Salsa and K-pop dance use `dance.jpg`).
Give them their own photo by changing `photo` and `alt` in `index.html`.

Each photo has alt text in `index.html` (the `alt` field of each class) that describes the shot above.
If your photo shows something else, update its alt text so screen readers describe the real picture.

For a Wix embed, set `PHOTO_BASE` in `index.html` to your GitHub Pages address, for example
`https://YOUR-USERNAME.github.io/sidequest/images/`, so Wix can find the photos.

## Pages and features

- **Home, Classes, Booking, Confirmation, My bookings**, plus the **Hobby quiz**, **Reviews** for each class, **Teach on Sidequest**, and the **Terms**, **Privacy** and **Refund** pages (linked in the footer and under "Book now").
- **Hobby sections:** classes are grouped by type (Creative, Sports, Music, Movement, plus Other for new teacher hobbies). "Filter by type" narrows the hobby chips.
- **Spots:** every booking takes a spot, and the count drops everywhere (class cards, calendar, booking form, confirmation). Cancelling gives the spot back.
- **Bring a friend:** books a second spot under the friend's own email; their first class is free too, and they get their own confirmation email. It needs 2 spots left. Cancelling the booking cancels both spots.
- **Same time every week:** keeps the same spot for 4, 6 or 8 weeks. The confirmation lists the dates, and "Add to Google Calendar" adds a repeating event. Pay per class, cancel any week.
- **No match (error state 1):** when nothing fits the filters, the page offers the same class at other times ("But there are spots on:"), then up to 3 similar classes on the day the person picked ("Or try something similar on Tuesday:"). Similar means, in order: the same class at another level, the same hobby, the same section (Movement, Sports, Music, Creative). Unrelated classes only show when nothing similar runs that day. Every section has at least one class every day, so a section filter always gets a match on that day.
- **Favourites:** a heart on every class card (and on quiz results) saves the class. "Saved (n)" on the Classes page shows only saved classes, and My bookings lists them with their next free time. Saved classes stay in this browser.
- **Hobby quiz:** its own page (`#quiz`), opened from "Not sure? Take the quiz" in the hero, the "Wanna try something but don't know what?" box at the bottom of the home page, and the footer. 4 questions (what sounds best, energy, experience, free time), one at a time, then the 3 best-matching classes, one per hobby when possible, each with its next free time. Scoring: section +4, energy +2/+1, level +3/+1/-2, a time in their free window +2, rating breaks ties. Each hobby's energy level is in `ENERGY` in `index.html`.
- **Remind me when a slot opens:** full times say "full · Remind me", and error state 1 offers "Remind me when a new … time opens". A reminder fires when someone cancels a spot in a full class, or when a teacher adds a matching class. It's emailed through the notice template, or shown as a note on the page while emails are off. Reminders are listed in My bookings.
- **Teach on Sidequest:** a teacher adds their name, a line about them, and a class (hobby, type, level, description, place, what to bring, up to 3 times, length, price with guidance, optional photo). The class and any new hobby appear on the site straight away (in the real service, the team checks new classes within 48 hours, story 3.1). Learners never see the teacher's email. Teachers can remove their classes from the Teach page.
- **404 page:** a broken link inside the site (like `#banana`) shows "This quest doesn't exist." with bouncing 404 tiles, "Back to home", "Let fate pick a hobby" and 4 random hobbies to try. `404.html` is the same page for addresses GitHub Pages can't find; its buttons find the site's home on their own (a project page like `/sidequest/`, or the root of a domain).
- **Cookie banner:** shows on the first visit, with "Only necessary" and "Accept analytics" side by side. The choice is saved in the browser (see Analytics hooks below).
- **Policies:** plain-language drafts. Fill in `[team email]` and `[name]`, and have them checked before real use. The Privacy page has a working "Delete my data on this device" button.

## Calendar

- On the Classes page, **List / Calendar** switches between class cards and a calendar of the next 7 days.
  Every filter (hobby, level, day, time, search) works in both views, and tapping a time in the calendar opens the booking.
- **Filter by time**: morning (before 12pm), afternoon (12–5pm) and evening (after 5pm). This is the CP1 decision-phase fix:
  "a calendar and time filters" so Nora finds a slot around her Tuesday lab faster.
- After booking, **Add to Google Calendar** (confirmation page and My bookings) opens Google Calendar with the class, time, place and what to bring filled in.
- Class lengths are placeholders: 1 hour, or 1.5 hours for pottery, wheel throwing, sewing, figure drawing and terrariums (`mins: 90`).

## Reviews

- Every class has a rating and a reviews page (open it from "Read reviews" on a class). Classes a teacher adds on the Teach page start with "No reviews yet".
- The starting reviews are samples written for the demo.
  The reviews page says that every review without a "Your review" tag is a sample, and the counts say "sample reviews".
  Replace them in `SAMPLE_REVIEWS` in `index.html` with real reviews; keep the note while any invented text is still there.
- Anyone who booked a class with an email can review it with that email. Someone without a booking is told
  "You can only review classes you've booked" (the unhappy path from the review story).
- Posting a first review for a class gives 10% off the next paid class for that email (the CP1 return-phase measure).
- Reviews are saved in the visitor's own browser only, like bookings.

## Placeholders to swap for real ones

All in the `CLASSES` list and the constants below it in `index.html`:
- Every teacher except Emma (dance), Nahema (guitar) and Sabina (ice skating). Founders are marked with `founder: true`.
- Every class added after the first 14 (Mateo, Ji-woo, Arjun, Félix, Yasmine, Gabriel, Mei, Olivier, Lina, Alexis, Rosalie, Théo, Élodie, Simone, Laila, Noah), with their places.
- Every time, spot count and price ($8–14).
- Where each class is held (the `where` field of each class: venue type and neighbourhood) and the note about the exact address (`WHERE_NOTE`).
- Cancellation terms (`CANCEL`).
- Error state 1 depends on tennis having no Tuesday class (it offers Thursday · 6pm and Saturday · 3pm), and error state 2's example uses Dance with Emma (Monday · 5pm and Wednesday · 7pm). Keep those if you want the site to match the CP2 drawings. The site also adds a "something similar on Tuesday" part below those two times, which the CP2 drawing doesn't show.

Bookings and the log-in are saved only in each visitor's own browser (localStorage). There's no database behind the demo.

## Design system v2 (for Parts C and D)

Type keeps the CP2 sizes: main title 80px, subtitles 28px, buttons 24px, body 18px, and nothing smaller than body.
Headings use Unbounded, body text uses Figtree. Spacing base unit: 8px (8, 16, 24, 32, 48, 64, 96).

| Role | Text | Background | Contrast |
|---|---|---|---|
| Body text | `#1A1430` | `#FAF7FF` | 16.69:1 |
| Text on light violet | `#1A1430` | `#D9CCFF` | 11.82:1 |
| Text on light green | `#1A1430` | `#CFF7B5` | 14.85:1 |
| Main buttons | `#CFF7B5` | `#1A1430` | 14.85:1 |
| Secondary text | `#4E4766` | `#FAF7FF` | 8.19:1 |
| Secondary text on light violet | `#4E4766` | `#D9CCFF` | 5.80:1 |
| Links and focus ring | `#6236E8` | `#FAF7FF` | 6.16:1 |
| Not allowed | `#6236E8` | `#D9CCFF` | 4.36:1 (fails) |

Extra colours, always with `#1A1430` text: pink `#FFC2DC` 11.79:1, yellow `#FFE98A` 14.55:1, blue `#BFE5FF` 13.37:1, peach `#FFCBA4` 12.07:1.
Ratios are cut at two decimals, never rounded up.

## Analytics hooks

Analytics only run after a clear yes in the cookie banner (Québec's Law 25). Until then nothing is sent, and "Only necessary" is as easy to pick as "Accept analytics".
"Cookie settings" in the footer (and on the Privacy page) lets people change their choice; "Delete my data on this device" forgets it.

**Checkpoint 3:** paste your GA4 Measurement ID into `GA_ID` near the top of the script in `index.html` (for example `"G-ABC123XYZ"`).
Google Analytics then loads only for people who accept, with Google Consent Mode set to "denied" by default.
Saying no later switches it off again and removes the `_ga` cookies.

Once someone accepts, the site sends these events with `gtag("event", …)`:
`book_class_click` (objective 1 signal), `booking_page_view` and `booking_complete` (objective 2, booking completion rate),
`filter_no_results`, `already_booked_shown`, `confirmation_email_sent`, `confirmation_email_failed`, `spin`, `login`,
`calendar_view`, `add_to_calendar`, `reviews_page_view`, `review_submitted`, `reminder_set`, `reminder_fired`, `class_listed`,
`favourite_add`, `favourite_remove`, `saved_filter`, `quiz_open`, `quiz_complete`, `quiz_restart`, `page_not_found`, `not_found_random`.

## AI use

This code was written with Claude (Anthropic). Declare it in the AI appendix of the next checkpoint.
