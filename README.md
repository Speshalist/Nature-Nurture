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

### Local deploy option

```bash
npm run build
npx wrangler deploy
```
