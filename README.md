# Nature-Nurture

A website for our new SING group.

## Contact Form (Web3Forms)

The "Send Us a Message" form is wired to Web3Forms, similar to bowl29.com.

### Setup

1. Create a form at Web3Forms and get your Access Key.
2. Create a `.env` file in the project root.
3. Add this value:

```bash
PUBLIC_WEB3FORMS_ACCESS_KEY=your_access_key_here
```

4. Run locally with `npm run dev` and test the form.
5. For hosting, add `PUBLIC_WEB3FORMS_ACCESS_KEY` as an environment variable in your deployment platform.

If the key is missing, the form shows a clear "not configured" message instead of failing silently.

## Deploy to Cloudflare Workers

This repo is configured for Cloudflare Workers static asset hosting using `wrangler.jsonc`.

### One-time Cloudflare setup

1. In Cloudflare dashboard, go to **Workers & Pages**.
2. Create a new Worker project connected to this GitHub repository.
3. Set build command to `npm run build`.
4. Ensure the asset directory is `dist` (also defined in `wrangler.jsonc`).
5. Add environment variable `PUBLIC_WEB3FORMS_ACCESS_KEY` in Worker settings.

### Deploy

1. Commit and push to `main`.
2. Cloudflare will rebuild and deploy automatically.
3. Add your custom domain in Worker settings when ready.

### Newsletter signup (Mailchimp)

The newsletter form now submits to a configurable Mailchimp signup URL.

1. Copy your Mailchimp signup form action URL from the embed form code.
2. Create a `.env` file in the project root.
3. Add this value:

```bash
PUBLIC_MAILCHIMP_FORM_ACTION_URL=https://your-list.us1.list-manage.com/subscribe/post?u=your_u_value&id=your_id_value
```

4. Run locally with `npm run dev` and test the form.
5. For hosting, add `PUBLIC_MAILCHIMP_FORM_ACTION_URL` as an environment variable in your deployment platform.

### Mailchimp footer layout (Manage Preferences first)

Because Meditation and SING are in the same Mailchimp audience, use a footer that encourages people to update preferences before unsubscribing from everything.

#### Recommended structure

1. Put **Manage Preferences** first.
2. Make **Manage Preferences** larger or bold.
3. Explain that preferences let subscribers stay in one group while leaving another.
4. Keep the required **Unsubscribe** link smaller and below the preferences link.

#### Copy/paste footer block

Paste this into your Mailchimp email footer content block:

```html
<p><strong>Changed your mind?</strong></p>
<p>
	If you want to leave just one of our groups (like Meditation) but stay enrolled in the other (like SING),
	please <strong>*|UPDATE_PROFILE|*</strong>.
</p>
<p style="font-size: 0.9em; opacity: 0.9; margin-top: 0.5rem;">
	If you choose to <strong>*|UNSUB|*</strong>, you will be completely removed from both communities.
</p>
```

Notes:
1. `*|UPDATE_PROFILE|*` renders as your Manage Preferences link in Mailchimp.
2. `*|UNSUB|*` renders as your mandatory unsubscribe link.
3. Keep both merge tags in the footer to remain compliant.

#### Where to add it in Mailchimp

1. Open your Mailchimp email template (or campaign builder).
2. Click the Footer content block.
3. Replace the existing footer text with the block above.
4. Preview and send a test email.
5. Confirm the preferences link opens profile/preferences and unsubscribe removes all emails.

### Local deploy option

```bash
npm run build
npx wrangler deploy
```
