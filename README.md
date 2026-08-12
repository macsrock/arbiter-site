# arbiter.xyz

Marketing site for **Arbiter** — a self-custody Arbitrum wallet with Hyperliquid
perpetuals built in.

Static HTML, no build step. `index.html` carries its own CSS inline; the two
legal pages share `assets/legal.css`.

```
index.html      landing page
terms.html      terms of service (fee disclosure lives in §2)
privacy.html    privacy policy
assets/         logo, favicon, og card, app screenshots
CNAME           arbiter.xyz
```

## Local preview

```
python3 -m http.server 8787
```

Then open http://127.0.0.1:8787 — opening `index.html` straight off the disk
works too, but the OG tags reference absolute URLs.

## Deploying

GitHub Pages serves `main` at the repository root. Pushing to `main` publishes;
there is no workflow to wait on beyond Pages' own build.

## DNS

The domain is registered at GoDaddy, but at the time of writing its nameservers
were delegated to `ns1/ns2.eftydns.com` — a parking service left over from the
acquisition. **Records added in GoDaddy's DNS panel have no effect until the
nameservers are switched back to GoDaddy's own.**

Once they are, the apex needs four A records pointing at GitHub Pages:

```
@    A       185.199.108.153
@    A       185.199.109.153
@    A       185.199.110.153
@    A       185.199.111.153
www  CNAME   macsrock.github.io
```

Delete the parking record (`86.105.245.69`) at the same time. GitHub issues the
TLS certificate automatically once the apex resolves, usually within an hour;
tick **Enforce HTTPS** in the repository's Pages settings after it appears.

## Note on the legal pages

`terms.html` and `privacy.html` were drafted to describe what the app actually
does — including the 0.01% builder fee, which the app no longer discloses via a
popup. They have not been through legal review.
