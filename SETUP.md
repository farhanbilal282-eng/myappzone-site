# MyAppZone — setup (about 15 minutes)

The site is plain HTML/CSS/JS (no build step). It uses your Supabase project for login, the apps database, image storage and contact messages.

## 1. Database (already done)
`supabase/schema.sql` has already been applied to your Supabase project "Smart Business" (all tables start with `maz_`, nothing else was touched). If you ever use a different project, paste that file into Supabase → SQL Editor → Run.

## 2. Make yourself the admin  (required, once)
1. Open the website → Login → **Sign up** with your own email, confirm the email.
2. Supabase → SQL Editor → run (use your email):
   `insert into public.maz_admins (email) values ('you@example.com') on conflict do nothing;`
3. Open `/admin.html` — the dashboard now works. Anyone else sees "Admin access only", and the database rejects their changes too.

## 3. Google login (needed for "Continue with Google")
1. Google Cloud Console → APIs & Services → Credentials → Create **OAuth client ID** (Web application).
   Authorized redirect URI: `https://zzoahqybtbowlstvrkwt.supabase.co/auth/v1/callback`
2. Supabase → Authentication → Providers → Google → enable, paste Client ID + Secret.
3. Supabase → Authentication → URL Configuration:
   Site URL `https://www.myappzone.online` and add Redirect URL `https://www.myappzone.online/login.html` (and `https://www.myappzone.online/**`).
Email/password login works without Google.

## 4. Upload the website
Upload the whole folder contents to your host root (the `myappzone.online` web root): `index.html`, `apps.html`, `app.html`, `login.html`, `admin.html`, `about.html`, `contact.html`, `privacy.html`, `terms.html`, `404.html`, `css/`, `js/`, `assets/`, `sitemap.xml`, `robots.txt`.
Set your host's 404 page to `404.html`. HTTPS is required.
`js/config.js` already holds your Supabase URL and public key (safe to be public; security comes from the database rules).

## 5. Add your apps
Admin → **+ Add new app**: name, descriptions, features, icon, screenshots, **Open URL** and **Live Demo URL** (separate). Save draft, Preview, then Publish.
- **Open** → visitor must log in; after login they are sent to the Open URL. The Open URL is stored where only logged-in users can read it.
- **Live Demo** → goes straight to the demo URL, no login.
Important: logging in to MyAppZone does not log a visitor into an external app. If your app has its own accounts, it still asks for its own login (or protect it on its own server).

## Things to know
- Contact messages are stored in the database; read them in Admin → Messages. They are not emailed automatically.
- Email confirmation setting: Supabase → Authentication → Providers → Email.
- `sitemap.xml` lists the main pages; add individual app links if you want them indexed.
