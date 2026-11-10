# GitHub Pages deployment

`index.html` is the canonical, latest approved website. It is a standalone HTML
file with embedded photos. The older `ARG-Renovation-v2.html` is retained for
history and is not the deployment entry point. Do not replace index.html with it.

## Enable Pages (one time)

Open https://github.com/anastasiiakolis-coder/arg-renovation/settings/pages.
Under Build and deployment choose **Deploy from a branch**, branch **main**,
folder **/(root)**, then Save. `.nojekyll` keeps publication buildless; there are
no application dependencies, third-party scripts or custom Actions workflows.

Set **Custom domain** to `argrenovation.ca` and Save before changing DNS.
The root `CNAME` file contains that domain. GitHub settings are authoritative;
a CNAME file alone does not prove Pages is enabled or a certificate is issued.

## Namecheap DNS (owner action)

Namecheap → Domain List → argrenovation.ca → Manage → Advanced DNS → Host Records.
These entries apply when Namecheap is the authoritative DNS provider; if the
nameservers point elsewhere, make equivalent changes at that provider instead.

| Type | Host | Value | TTL |
|---|---|---|---|
| A | @ | 185.199.108.153 | Automatic |
| A | @ | 185.199.109.153 | Automatic |
| A | @ | 185.199.110.153 | Automatic |
| A | @ | 185.199.111.153 | Automatic |
| CNAME | www | anastasiiakolis-coder.github.io | Automatic |

Replace conflicting parking/URL redirect records only for @ and www. Preserve
email MX/TXT records and unrelated subdomains. Do not create a wildcard record.
For optional IPv6, add all four GitHub Pages AAAA addresses:
2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153,
2606:50c0:8003::153. Remove conflicting old AAAA records for the same host.

For additional takeover protection, verify domain ownership in your GitHub
account Settings → Pages using the exact TXT token GitHub generates. Do not
invent or reuse a sample token. Keep the verification TXT record afterward.

After DNS resolves, wait for GitHub's DNS check/certificate and enable **Enforce
HTTPS** when available. Verify https://argrenovation.ca and
https://www.argrenovation.ca, with www redirecting to the apex. DNS can take
up to 24 hours; certificate issuance may take additional time. Publication,
DNS, redirects and HTTPS must be checked live, not inferred from these files.

## Future approved changes

Ask Codex to branch from main and edit index.html. Review the preview and merge
the approved pull request into main. Once Pages uses main /(root), GitHub
rebuilds/deploys automatically after each push/merge; no manual upload or npm
build is needed. Preserve CNAME, .nojekyll and embedded images. Test the review
carousel, image viewer, email/phone/SMS links and mobile layout before merging.
Never commit local backups, screenshots, uploaded ZIPs, credentials or audit
scratch files. Local source copies outside this repository are not automatically
published. Changes must reach index.html in main.
