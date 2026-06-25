# Rolodex — installable PWA

A private, fully offline notebook for remembering the people you meet:
their work, likes, dislikes, birthday, phone number, and how you know them.

No account. No server. No data ever leaves your device unless you choose
to back it up.

---

## ⚠️ Project status: Dropped

After building and UAT-testing this app, the project has been discontinued. The core reason is that it does not offer meaningful value over what already ships on every Android phone.

**Google Contacts and Samsung Contacts already provide:**
- Automatic, continuous sync across all devices
- Birthday reminders via Google Calendar
- Photos, multiple phone numbers, emails, and addresses per contact
- Integration with the phone dialer, WhatsApp, and Gmail
- Built-in duplicate detection
- Zero setup — already installed

**What Rolodex does differently:**
- Dedicated fields for Likes, Dislikes, and "how you met" — but these
  can simply be put in the Notes field of any contacts app.
- Tags (Friend, Work, Family…) — Google Contacts has Labels that do the same.
- Data never leaves the device — the only genuine differentiator, and
  only relevant if you specifically distrust Google with your contacts.

**What would have made it genuinely useful** is leaning into the
personal-CRM angle that Google Contacts does *not* cover: interaction
history ("last spoke 3 months ago"), reach-out reminders, pre-meeting
context prompts, and life-event tracking. Without those features this
is just a contacts app with fewer capabilities and a worse backup story.

The code and UAT results are preserved here for reference.

---

## How to install on your Android phone

1. Copy this whole folder to anywhere on your phone, **or** host it (see
   "Hosting options" below) — either way you need these 5 items together
   in one folder:
   - `index.html`
   - `manifest.json`
   - `service-worker.js`
   - `icons/` (folder with 4 PNGs)

2. Open `index.html` in **Chrome** on your phone.

3. You'll see an **"Install app"** button appear in the top right of the
   app itself — tap it, then tap **Install** in the prompt that pops up.
   (If you don't see the button, open Chrome's **⋮ menu → Add to Home
   screen**, which does the same thing.)

4. Rolodex now lives on your home screen like any other app — full
   screen, its own icon, works with no internet connection.

### Hosting options (so installing is one tap, not a file copy)
A PWA installs more reliably when it's served over `https://` rather than
opened as a local file. Easiest free options:
- **GitHub Pages** — push this folder to a GitHub repo, enable Pages, done.
- **Netlify Drop** (netlify.com/drop) — drag the folder in, get a live URL
  in seconds, no account required for a quick test.
- **Vercel**, **Cloudflare Pages** — similar one-drag deploy flow.

Once hosted, just open that URL on your phone and install from there.

---

## Backing up to Google Drive

Open the **Backup** menu (top right) — there are two options:

- **Save to Drive…** — opens your phone's native share sheet and lists
  Google Drive as a destination (along with WhatsApp, Email, etc., if
  installed). Pick Drive, choose a folder, done. This uses Android's
  built-in sharing, so there's no login or setup needed inside the app
  itself — it relies on you already being signed into Drive on your
  phone.
- **Export to file** — saves the backup `.json` file to your phone's
  Downloads folder, in case you'd rather move it manually.

Your backup is a single `.json` file containing everyone's details.
**Restore it anytime** via **Backup → Import from file** — you'll be
asked whether to merge it with what's already on the phone, or replace
the list entirely.

> Because this is a share-sheet-based backup (not a live, automatic Drive
> sync), it backs up at the moment you tap "Save to Drive," not
> continuously. Get in a habit of doing it after a few new entries, or
> right before switching/upgrading phones.

---

## Notes on this approach vs. a "real" Drive-synced native app

This PWA gives you:
- ✅ A real, installable, full-screen, offline app
- ✅ One-tap backup into Drive via the OS share sheet
- ✅ Zero accounts, zero servers, zero ongoing cost
- ✅ Works today, no Play Store review wait

It does **not** give you:
- ❌ Automatic background sync to Drive (it's backup-on-demand, not live sync)
- ❌ A Play Store listing
- ❌ Cross-device sync without manually moving the backup file

If later on you want automatic Drive sync or a Play Store listing, that's
a native Android (or Flutter) project using the Google Drive API with
OAuth — a meaningfully bigger build that needs a Google Cloud project,
a Play Console account, and proper app signing. Happy to write that
version's source code if you decide to go there.
