# Sidequest

Beginner hobby classes in Montreal, taught by students. First class free, then pay per class.
Group 6 project for INSY 440 E-Business, McGill, Fall 2026.

The whole site is one file, `index.html` (HTML, CSS and JavaScript together), so it can be opened directly,
hosted on GitHub Pages, or pasted into a Wix **Embed code** element.

## What's in the repo

| File | What it is |
|---|---|
| `index.html` | The site: Home, Classes, Booking, Confirmation and Profile |
| `email/confirmation-template.html` | The booking confirmation email, to paste into EmailJS |
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
5. In `index.html`, find `const EMAIL = {` and replace the three `YOUR_...` values. Commit and push.

How it behaves:
- While the three values are still `YOUR_...`, the confirmation page says emails aren't switched on and shows every detail on screen.
- If sending fails (no connection, wrong ID, monthly limit reached), the page says so, keeps the booking, shows every detail and offers **Try again**. This is the unhappy path from story 2.3.
- The claude.ai preview of the site blocks outside connections, so emails only go out from GitHub Pages (or Wix).

Because the recipient comes from the form, anyone who opens the page can trigger an email to an address they type.
That's fine for a class demo; for real use, add reCAPTCHA in EmailJS or send emails from a server.

## Placeholders to swap for real ones

All in the `CLASSES` list and the constants below it in `index.html`:
- Teachers for tennis (Sabina), pottery (Viktorie) and photography (Man Ning). Dance with Emma and Guitar with Nahema come from the CP2 audit.
- Every time, spot count and price ($8–12, from the interview price range).
- Cancellation terms (`CANCEL`) and the location line (`WHERE`).

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

The site pushes events to `window.dataLayer`, ready for GA4 in Checkpoint 3:
`book_class_click` (objective 1 signal), `booking_page_view` and `booking_complete` (objective 2, booking completion rate),
`filter_no_results`, `already_booked_shown`, `confirmation_email_sent`, `confirmation_email_failed`, `spin`, `login`.

## AI use

This code was written with Claude (Anthropic). Declare it in the AI appendix of the next checkpoint.
