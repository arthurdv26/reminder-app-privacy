# Reminders CL Privacy Website

A simple, production-ready static website for the Reminders CL mobile app by Cloud Lab. It hosts the official Privacy Policy at `https://reminders.cloudlab.name/privacy-policy` for use on Google Play.

## Project structure

```text
./
├── index.html                # Landing page for Reminders CL
├── privacy-policy/
│   └── index.html            # Privacy Policy page
├── delete-account/
│   └── index.html            # Google Play Delete Account URL page
├── assets/
│   └── style.css             # Shared stylesheet
├── _headers                  # Cloudflare Pages security headers
├── vercel.json               # Vercel rewrite for /privacy-policy
└── README.md                 # This file
```

## What this project is

This is a no-build, no-backend static site designed for Cloudflare Pages. It contains:

- A branded landing page for Reminders CL.
- A complete Privacy Policy for the Reminders CL mobile app.
- SEO meta tags and a canonical URL for the Privacy Policy.
- Sensible Cloudflare Pages security headers that do not block search crawlers.

## Deployment to Cloudflare Pages

1. Log in to the [Cloudflare dashboard](https://dash.cloudflare.com/).
2. Go to **Pages** → **Create a project**.
3. Choose your upload method:
   - **Direct upload**: zip the project root and upload it.
   - **Git integration**: connect the repository and set the build output directory to the project root (no build command is needed).
4. Cloudflare Pages will serve the static files directly.
5. Verify the deployment by visiting `https://<your-pages-subdomain>.pages.dev/privacy-policy/`.

## Deployment to Vercel

If you deploy this repo to Vercel, `vercel.json` at the project root rewrites `/privacy-policy` to `privacy-policy/index.html` and `/delete-account` to `delete-account/index.html`. No extra build settings are required.

## Custom domain: `reminders.cloudlab.name`

1. In the Cloudflare Pages project, go to **Custom domains**.
2. Click **Set up a custom domain** and enter `reminders.cloudlab.name`.
3. Cloudflare will prompt you to add a CNAME DNS record. In the `cloudlab.name` DNS zone, add:

   ```
   Type: CNAME
   Name: reminders
   Target: <your-pages-subdomain>.pages.dev
   Proxy status: Proxied (orange cloud)
   TTL: Auto
   ```

4. Wait for certificate issuance and DNS propagation, then verify `https://reminders.cloudlab.name/privacy-policy` loads.

## Replace the contact email placeholder

Before production deployment, replace `[PRIVACY_CONTACT_EMAIL]` with the real support/privacy email address in these files:

```text
privacy-policy/index.html
delete-account/index.html
```

Search each file for `[PRIVACY_CONTACT_EMAIL]` and update both the `href` value and the link text. **This placeholder must be replaced before submitting the URL to Google Play.**

## Final Google Play URLs

Enter this URL into the Google Play Console as the **Privacy Policy URL**:

```text
https://reminders.cloudlab.name/privacy-policy
```

Enter this URL into the Google Play Console as the **Delete Account URL**:

```text
https://reminders.cloudlab.name/delete-account
```

## Notes

- No build step, Node.js, npm, Docker, or backend server is required.
- Do not add a `robots.txt` rule that blocks `/privacy-policy`; Google Play and other crawlers must be able to access it.
- Do not invent a physical address or phone number; only the email placeholder should be replaced.
