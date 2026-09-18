# ShqipFilma

This project is a static HTML site that can be published with either GitHub
Pages or Cloudflare Workers Static Assets.

## Publish with GitHub Pages

1. Create a GitHub repository and push this folder to the `main` branch.
2. In the repository, open **Settings > Pages**.
3. Set **Source** to **GitHub Actions**.
4. Push a change, or run **Actions > Deploy to GitHub Pages > Run workflow**.

The workflow in
[`./.github/workflows/deploy-pages.yml`](./.github/workflows/deploy-pages.yml)
will publish the repository root and display the public URL in the workflow
environment. For a project repository, the default URL is:

```text
https://YOUR-USERNAME.github.io/YOUR-REPOSITORY/
```

For a custom domain, add a `CNAME` file containing only the domain name and
configure the DNS records described by GitHub. Do not commit credentials or
API keys.

## Publish with Cloudflare Workers

1. Install Node.js LTS.
2. From this folder, authenticate Wrangler:

   ```powershell
   npx wrangler login
   ```

3. Deploy the site:

   ```powershell
   npx wrangler deploy
   ```

Wrangler will print the public `workers.dev` URL. To use a custom domain, add the
domain in the Cloudflare dashboard under **Workers & Pages**, then configure the
route or custom domain for the `shqipfilma` Worker.

## Important production limitations

- Published content, accounts, favorites, ratings, and history are currently
  stored in browser `localStorage`/`sessionStorage`. They are not shared between
  visitors or devices. A shared catalogue and real authentication require a
  server-side API plus D1/R2 (or another database/storage service).
- The admin credentials are present in the client-side JavaScript and therefore
  cannot be treated as a secret. Do not use this admin system for sensitive
  content or accounts until authentication is moved to a Worker API.
- The player loads third-party embed URLs directly in an iframe. A provider
  controls whether its content can be embedded and whether it is reachable from
  a visitor's network. Cloudflare deployment cannot legitimately override
  provider `X-Frame-Options`, CSP, geo restrictions, or network blocks. Use
  provider-approved embed URLs and obtain the necessary rights to distribute
  the content.

## Local preview

After installing Node.js, run:

```powershell
npx wrangler dev
```

Then open the local URL Wrangler prints.
