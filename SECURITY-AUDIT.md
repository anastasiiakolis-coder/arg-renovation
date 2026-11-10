# Security review — 2026-11-09 (America/Halifax)

## Scope and limits

Reviewed a fresh, non-shallow mirror of every ref advertised by GitHub at audit
time: 7 branches, 9 reachable commits, 9 distinct file blobs. No tags or pull
request refs were advertised. Files across those commits: ARG-Renovation-v2.html
and README.md. Hidden files, symlinks, submodules, Actions workflows and dependency
manifests were absent. Git object integrity checking passed.

Also reviewed the latest owner-approved local standalone HTML selected as the
new index.html, including the Instagram link, review carousel and garage-photo
viewer. index.html is byte-for-byte identical to that approved source; no design,
copy, photo or layout was changed for publication.

This covers advertised/reachable history, not deleted refs, GitHub-internal
unreachable objects, other forks, previous clones, account settings, Actions
secret values, private Namecheap data or a guarantee against every possible
secret format. No claim is made that GitHub Pages or DNS was activated.

## Findings

| Location | Finding / impact | Treatment |
|---|---|---|
| Git author/committer metadata in historical commits | A personal author email is public. It is not a business website contact and may be unintended personal information. | History preserved. Owner must decide whether to keep it or explicitly authorize history rewriting. Configure GitHub email privacy / noreply for future commits. Existing public copies cannot be recalled by rewriting. |
| main:ARG-Renovation-v2.html | Old content, visible unfilled placeholders and incomplete Taskrabbit links; unsuitable as the current production entry point. | Historical file retained. New index.html uses the latest approved complete website instead. |
| Repository root before preparation | No index.html or Pages custom-domain/source files. | Added index.html, .nojekyll and CNAME for a buildless main-root Pages deployment. Pages activation still requires repository settings. |
| Local working directories (outside tracked repository) | ZIP uploads, screenshots, backups and review drafts exist locally. Accidentally committing them would expose unnecessary data. | None were copied into this publication commit. Added focused .gitignore exclusions for credentials, archives and local review/backup folders. |

## Checks without findings

- Typical private-key blocks, GitHub/AWS/Google/Slack/Stripe token formats,
  quoted credential assignments, credential-bearing URLs and JWT-like values:
  no matches in reachable file contents or commit messages. Embedded image
  payloads were decoded and inspected separately rather than treated as text.
- All 22 unique embedded raster images in repository history decode. No EXIF
  tags, GPS IFD or XMP entries were found. Publication source image metadata was
  checked independently; the 11 stored payloads contain no EXIF/XMP. The page
  renders 12 content images by sharing the shed image plus an empty viewer image
  that receives a source only when opened.
- No domestic street address, identity/financial/registration document or
  additional personal phone/email was found in file text. The only file contact
  details are the owner-approved business phone and Gmail address.
- Historical image inventory was visually reviewed: logo, Roman portrait and
  supplied project photos; no uploaded review screenshots or documents are
  stored as image payloads in the repository. Photos can still identify a
  property visually; client permission remains the owner's responsibility.
- No remote script imports, dependencies, eval, cookie/local-storage usage,
  tracking requests, forms or user-input processing in the publication source.
  Taskrabbit and Instagram use HTTPS and noopener on new-tab links. The
  website does not receive or store customer messages; mailto/tel/sms open
  the visitor's configured applications.
- No custom Actions workflow or build dependency is introduced. Branch-based
  GitHub Pages publication uses only GitHub's own infrastructure.

## Business information intentionally retained

782-882-3213; a.r.g.renovation.ca@gmail.com; Roman's business portrait; project
photographs; service area; public Taskrabbit profile and Instagram handle.
These were previously supplied/approved for the public website. They are not
secrets to delete automatically.

## Functional checks of publication source

Chromium at 390, 768 and 1440 px: garage photos open and close in the viewer,
review carousel advances, responsive review height updates, Instagram link is
clickable with the exact supplied target, no horizontal page overflow and no
JavaScript errors. Earlier same-source standalone checks confirmed all content
images load without an images/ folder and mailto/tel/sms/Taskrabbit destinations
are correct. This is not an iPhone Safari or live-production test and did not
send email, SMS, place calls or authenticate to external profiles.

## Live configuration limitations

The available GitHub connector reports repository admin/write permissions but
provides no Pages-settings tool. REST calls to api.github.com and HTTP access
to the github.io site were denied by this environment's egress policy. Local
DNS lookups failed. The shared-browser settings attempt also failed. Therefore
Pages enabled/source state, domain ownership, authoritative DNS, certificate
issuance, redirects and HTTPS enforcement could not be confirmed or changed.
Namecheap settings were not accessed or modified. See DEPLOYMENT.md for exact
owner actions. No other hosting provider was used.
