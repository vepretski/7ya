# 7YA Digital Integration Architecture

Status: implementation contract, public-safe draft.  
Date: 2026-06-21.  
Scope: 7ya.io lightweight command hub, not a WordPress or WooCommerce migration.

## Core decision

7ya.io remains the central public command hub for Igor Vepretski / #7YA / StartOn.

Do not migrate the core site to WordPress. Do not add WooCommerce. Do not add plugin-heavy architecture. WordPress, if used later, is only a secondary content satellite.

## Route map

Required static routes:

- `/` existing public entry remains intact unless explicitly redesigned.
- `/starton/` social impact and sponsorship narrative.
- `/sponsor/` sponsor conversion page.
- `/media/` owned and external media routing.
- `/evidence/` evidence-first public claims archive.
- `/press/` press-safe identity kit.
- `/book/` scheduling gateway.
- `/drops/` digital products and releases.
- `/go/` internal Link-in-Bio routing hub.
- `/go/starton/`
- `/go/music/`
- `/go/media/`
- `/go/book/`
- `/go/evidence/`

## Commercial architecture

Use external checkout for digital products and paid consulting. Gumroad may be embedded as buttons or overlay placeholders.

Do not use Gumroad language for official nonprofit donations unless accounting/legal handling is confirmed. StartOn sponsorship and donations must remain separated from product sales.

## Kit / ConvertKit taxonomy

Only collect minimal lead data:

- email
- optional name
- source
- interest
- consent timestamp

Suggested tags:

- `source.youtube`
- `source.tiktok`
- `source.instagram`
- `source.linkedin`
- `source.search`
- `interest.starton`
- `interest.music`
- `interest.media`
- `interest.evidence`
- `interest.consulting`
- `intent.sponsor`
- `intent.book_call`
- `intent.buy_product`
- `stage.new`
- `stage.engaged`
- `stage.booked`
- `stage.sponsor_lead`
- `consent.email_yes`

No Kit API key may appear in client HTML, JavaScript, screenshots, public docs, or GitHub commits.

## Calendly flow

Calendly embeds may be placed on `/book/` and `/sponsor/` as placeholders until the final scheduling URL is supplied.

Recommended event types:

- StartOn sponsor call
- Media / podcast booking
- 7YA consulting call
- Press inquiry
- Collaboration call

Every booking should create or update a CRM subscriber with source and intent tags.

## Gumroad webhook flow

Supported events:

- sale
- refund
- subscription_cancelled
- dispute
- affiliate_sale

Minimum event handling contract:

1. Receive webhook server-side only.
2. Validate source and signature when available.
3. Normalize event into an append-only event record.
4. Update subscriber tags in Kit.
5. Never send AI-generated emails without human approval.
6. Never mix nonprofit sponsorship records with digital product sales.

## Human approval rule

AI may summarize, classify, draft, and recommend.

AI must not autonomously:

- publish site changes
- send emails
- change payment routing
- claim exposure metrics
- add partners or sponsors
- merge deployment branches
- delete evidence or archive data

## Evidence-first public language

Allowed metric statuses:

- `verified`
- `source_visible_pending_screenshot`
- `pending_source`
- `private_source_not_public`

Forbidden behavior:

- no invented reach
- no combined exposure totals
- no follower + view aggregation
- no fake partner logos
- no screenshot-free verification claims
- no artificial portraits presented as documentary evidence

## Analytics readiness

All `/go/*` pages should preserve UTM parameters where possible and use clear CTA labels:

- `cta_starton_sponsor`
- `cta_book_call`
- `cta_music_platform`
- `cta_evidence_archive`
- `cta_media_watch`
- `cta_digital_drop`

## Deployment rule

Work should land in a feature branch and PR first. Main publishes through GitHub Pages, so direct main pushes are production deploys and require explicit approval.
