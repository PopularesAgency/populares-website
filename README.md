# Populares holding website

A single-page holding site to use if the main Populares website goes down.

## Hosting

Served by **GitHub Pages** from the root of the `main` branch:

**https://popularesagency.github.io/populares-website/**

Pushing to `main` redeploys it automatically (usually within a minute or two).

## Previewing

- **Live:** open the URL above.
- **Locally:** open `index.html` in a browser, or run a local server from the repo folder:

  ```bash
  python -m http.server 8000
  ```

  then visit http://localhost:8000.

## Switching over in an emergency (Cloudflare redirect)

This sends visitors from the main domain to the holding site. It takes effect within about a minute and is easy to undo.

1. Log in to Cloudflare and open the **populares.co** zone.
2. Go to **Rules → Redirect Rules → Create rule**.
3. Name it something like `Holding site failover`.
4. Under **If incoming requests match**, choose **All incoming requests** (or a custom filter where *Hostname* equals `populares.co` or `www.populares.co`).
5. Under **Then**, choose:
   - **Type:** Static
   - **URL:** `https://popularesagency.github.io/populares-website/`
   - **Status code:** 302 (temporary)
   - Leave **Preserve query string** unticked.
6. Click **Deploy**.

> The DNS records for `populares.co` / `www` must be **Proxied** (orange cloud) for the redirect to apply.

Visitors will see the github.io address in their browser bar while the redirect is active.

### Switching back

When the main site is back up, go to **Rules → Redirect Rules** and toggle the rule **off** (or delete it). You can leave it disabled so it's ready for next time.
