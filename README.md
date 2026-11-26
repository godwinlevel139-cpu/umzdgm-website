# UMZDGM Website (Upon Mount Zion Deliverance Gospel Ministry)

A static website you own. Content lives in `content/site.json` in your GitHub repo. The admin dashboard at `/admin` (Decap CMS) edits that file and commits to GitHub; Netlify then rebuilds and publishes automatically.

## Files
- `index.html` public website (single page: Home, `#event`, `#watch`)
- `content/site.json` schedule, Mountain Experience sessions and livestream links, announcements, recordings, image paths
- `images/` logo, overseer photo, Mountain Experience banner, uploads
- `admin/` dashboard (`index.html`, `config.yml`)
- `netlify.toml` Netlify settings

## 1. Push to GitHub
1. Create a free GitHub account and **turn on two-factor authentication** (Settings > Password and authentication). This is your admin MFA.
2. Create a new **private or public** repository, e.g. `umzdgm-website`. Do not add a README.
3. Unzip this folder. In a terminal inside it:
   ```
   git init
   git add .
   git commit -m "Initial website"
   git branch -M main
   git remote add origin https://github.com/godwinlevel139-cpu/umzdgm-website.git
   git push -u origin main
   ```
   (No terminal? Use GitHub Desktop, or the repo page > Add file > Upload files, keeping the folder structure.)
4. Open `admin/config.yml` and change `repo:` to `godwinlevel139-cpu/umzdgm-website`. Commit and push.

## 2. Host on Netlify
1. Sign up at netlify.com with the same GitHub account.
2. Add new site > Import an existing project > GitHub > choose the repo.
3. Build command: leave empty. Publish directory: `.` Click Deploy.
4. Your site is live at `something.netlify.app`. Optional: Site configuration > Change site name.

## 3. Enable the admin login (one time)
1. GitHub > Settings > Developer settings > OAuth Apps > New OAuth App.
   - Homepage URL: your Netlify URL
   - Authorization callback URL: `https://api.netlify.com/auth/done`
   - Save, then generate a **client secret**.
2. Netlify > Site configuration > Access & security > OAuth > Install provider > GitHub. Paste the Client ID and secret.
3. Open `https://YOUR-SITE/admin/`, click Login with GitHub, authorise.
4. Only GitHub users you add as collaborators (repo Settings > Collaborators) can log in and publish. That is your roles system. Each save is a Git commit, which is your activity log.

## 4. Everyday editing (no code)
Go to `/admin/` > Website content. You can:
- change weekly services and times (Weekly schedule)
- add or edit Mountain Experience sessions, dates, times and **YouTube live links** (paste the YouTube live link or video ID; the player and Watch Live page update after publish, about a minute)
- add announcements and recordings (paste the YouTube link after each session)
- replace the banner, logo, overseer photo and add event photos

Tip: create the live broadcast in YouTube Studio ahead of time, copy its watch link, and paste it into that session. Visitors see the waiting room and then the live video.

Preview: uncomment `publish_mode: editorial_workflow` in `admin/config.yml`. Edits then become drafts with a Netlify deploy preview that you approve before publishing.

## 5. Custom domain
Netlify > Domain management > Add a domain. Register the domain in the church's own name and account (keep the registrar login with the church). Follow Netlify's DNS instructions. HTTPS is automatic.

## 6. Backup and restore
- Backup: your GitHub repo is the backup. Also run `git clone https://github.com/godwinlevel139-cpu/umzdgm-website.git` or download the repo ZIP monthly and store it safely.
- Restore: create a new repo from the backup, push it, and connect it to Netlify as in step 2. Or in GitHub, open an older commit and use Revert.

## 7. Transfer to another developer or host
1. Add the developer as a repo collaborator, or transfer the repo (Settings > Danger zone > Transfer).
2. To change host: the site is plain static files. Upload the folder to any static host (Cloudflare Pages, GitHub Pages, cPanel hosting) and repoint DNS. Only `/admin` needs a different OAuth setup on a new host.
3. Keep control of: the GitHub account/organisation, the Netlify account, the domain registrar and the YouTube channel.

## What this version covers, and what it does not
Covered: editable schedule, Mountain Experience dates/sessions/livestream links, announcements, recordings, banner/logo/photos, roles and MFA through GitHub, change history through Git.
Not covered yet (needs a server and database, planned as the next phase): editing every sentence and contact number from the dashboard, sermon library, bank details and giving categories, transfer notification verification, counselling bookings, partnerships, AI assistant knowledge base, SEO fields, site-level user management.
Until then, contact numbers and other text can be changed by editing `index.html` on GitHub.

## Counselling bookings, transfer notifications, partnerships and prayer requests
These are Netlify Forms and need no extra setup. After the first deploy, open Netlify > Forms to see each submission (counselling, transfer-notification, partnership, prayer-request). Turn on email alerts in Forms > Form notifications, and export to CSV when needed.
- **Verify a transfer:** match the notification (name, amount, date, reference, optional receipt) with your bank statement, then record it in your own books. Netlify only stores the notification; it does not confirm money.
- **Counselling:** call or WhatsApp the person to confirm; counselling hours come from the schedule you set.
- **Online giving (optional):** create a Paystack account in the church's name, paste the public key (pk_...) into Website content > Paystack public key, and view payments in the Paystack dashboard.
- Bank accounts, giving categories, counselling topics, sermons, partner options, phone numbers and social links are all edited in `/admin/` > Website content.
- Bank details and counselling data: only publish account details you want the public to see.

## AI assistant (chat button on every page)
The assistant is a Netlify Function (`netlify/functions/assistant.js`). It answers visitors using your live schedule, Mountain Experience sessions, bank details, contacts and the Q&A you write in `/admin/` > AI assistant knowledge.
1. Create an Anthropic API account in the church's name (console.anthropic.com), add a payment method, **set a monthly spend limit**, and create an API key.
2. Netlify > Site configuration > Environment variables > add `ANTHROPIC_API_KEY` = your key (and optionally `ANTHROPIC_MODEL` to change the model). Redeploy.
3. Test: open the site, click "Ask our assistant". If it says it is unavailable, check the variable name and view Netlify > Functions > assistant > logs.
The key stays on the server and is never shown to visitors. You own the key and can switch provider by editing the one function file. If the assistant is off, the rest of the website works normally.

## Redesign notes
The home page now has: hero, welcome, weekly services, Mountain Experience, watch live, about, leadership, activities, sermons, gallery, announcements, giving and partnership, contact with map, and footer. Edit the welcome message, about text and activity descriptions in `/admin/` > Website content. Gallery photos are added there too. The photo of Pastor Clement Momoh is cropped from the programme banner; replace `images/pastor-clement-momoh.jpg` with a higher-quality portrait when you have one.
