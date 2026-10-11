# LearnWith Himanshu — Blog Website

A responsive multi-topic blog built with React + Vite. Includes article search, topic filters, featured story, responsive layout, dark mode, reader modal, and an optional Supabase-powered publishing dashboard.

## 1. Run locally

Requirements: Node.js 20+ (Node 18.18+ may also work with compatible Vite versions).

```bash
npm install
npm run dev
```

Open the local URL Vite prints, typically `http://localhost:5173`.

Create a production build:

```bash
npm run build
npm run preview
```

## 2. Publish the static front end

Easy option: **Vercel** or **Netlify**.

1. Upload this project to a GitHub repository.
2. Import the repository into Vercel/Netlify.
3. Build command: `npm run build`
4. Output directory: `dist`
5. Deploy. These platforms provide a public URL; connect a custom domain later if you want one.

The front end works without a backend using its six sample articles. Newsletter form is currently a demo and does not store email addresses.

## 3. Enable real article publishing with Supabase (optional backend)

1. Create a project at https://supabase.com.
2. In Supabase SQL Editor, run the contents of `supabase-schema.sql`.
3. In Supabase Authentication, create your admin user. For a private one-person blog, disable public sign-ups after creating the admin user.
4. Copy `.env.example` to `.env.local` and fill in:
   - `VITE_SUPABASE_URL` = your Supabase Project URL
   - `VITE_SUPABASE_ANON_KEY` = your Supabase anon/publishable key
5. Restart `npm run dev`, or add these same environment variables to your hosting provider before deploying.
6. Open **Write** on the website and sign in with your Supabase admin credentials.

**Security note:** Never put a Supabase `service_role` or secret key in front-end environment variables. The browser should only use the anon/publishable key and Row Level Security (RLS). The sample SQL allows any authenticated user to manage posts, so for production you should restrict write policies to your specific admin user's UUID and keep public sign-ups disabled.

When Supabase is connected and contains published rows, the website loads them from the database. Posts created from the Write panel are stored in Supabase and are available across visitors/devices. If there are no published database rows, the site displays its sample posts.

## 4. Newsletter

The subscription form currently displays a demo message; it does not save email addresses. To collect real subscribers, connect a provider such as Buttondown, Brevo, Mailchimp, or a small serverless endpoint. Do not expose private API keys in React/browser code. A provider API key must be kept on a secure server/serverless function.

## 5. Before launch checklist

- Replace demo posts with your own reviewed articles.
- Add your own logo, About/contact details, privacy policy, and terms if needed.
- Configure a custom domain and HTTPS through your host.
- Add newsletter integration if you intend to collect email addresses.
- Tighten Supabase RLS policies to a specific admin account.
- Add analytics only if you need them and disclose tracking as required.
- Consider SEO metadata, sitemap, social sharing images, backups, and spam protections as the blog grows.

## Project structure

- `src/main.jsx` — React app and sample content
- `src/style.css` — responsive visual design
- `supabase-schema.sql` — optional database table and initial policies
- `.env.example` — environment variable template
