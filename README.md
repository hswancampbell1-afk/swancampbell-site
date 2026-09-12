# swancampbell.co.uk

The practice's one-page site. Static HTML, no build step, no dependencies —
edit `index.html` and push; GitHub Pages redeploys in about a minute.

`CNAME` holds the custom domain and is what tells Pages to serve it there.
Deleting it silently reverts the site to the github.io address.

Deliberately one page. A site does not win clients — conversations do — and
this exists so that a prospect who has already been pitched can look the
practice up and find something that reads as real.

Three claims on it are load-bearing and must stay true: that nothing is ever
sent without approval, that drafts may appear before they have been reviewed,
and that the Microsoft 365 permission does not include sending. All three are
properties of the software behind the service, not aspirations. If any stops
being true, this page changes the same day.

The third is the one most easily broken by accident, because it lives in
another repository. It is true because `MICROSOFT_SCOPES["email"]` in the
control panel is `Mail.Read`, `Mail.ReadWrite`, `User.Read` — creating a draft
and sending one are separate permissions in Microsoft Graph, and only the
first is held. Adding `Mail.Send` there would make this page false without
anyone touching this repository.

Note what the page does *not* claim. Google's `gmail.compose` is described by
Google as "manage drafts and send emails", so on Google the permission would
allow sending and only the software prevents it. The page says so. The
admission is why the Microsoft half is worth believing.

A fourth joined them on 12 September 2026, and it lives in that same other
repository. The pricing section says a pooled `+` tier gives you one shared
allowance across three mailboxes, so "a heavy mailbox draws on a quiet one's
headroom" — and `/audit` prices three mailboxes at three times the hours on
the strength of it. That is true because `plan_ceilings()` in the control
panel multiplies `PLANS` by `POOLED_MAILBOXES` for the two `+` tiers. It was
not true the day before: the pooled tiers shared one mailbox's ceiling
between three, which made Inbox+ strictly worse than buying three Inboxes at
the same price, and this page would have been selling a benefit that did not
exist. Reading ceilings off `PLANS` directly again — the obvious-looking
simplification, since that is where the numbers are — puts it back, and
nothing here would say so. Two tests in that repository hold the line:
`test_a_pooled_tier_is_never_worse_than_buying_the_solo_tier_three_times`
and `test_a_solo_tier_is_not_quietly_pooled`.

The pattern is now worth naming, since it has happened twice. Every claim on
this site that a prospect would find persuasive is a claim about software in
`vatools`, and neither repository's tests know about the other. The claims
survive because they are written down here next to the line of code that
makes them true, and because someone re-reads this file before changing
either.

## The share cards

`og-home.png` and `og-audit.png` are what LinkedIn, Slack and X render when
someone pastes a link. They are PNGs because those crawlers will not render an
SVG `og:image`, and one that silently fails is worse than none — the only
place on this site a raster file is unavoidable.

Both are generated from their `-card.html` source rather than drawn, so they
are the site's own tokens and the real Literata and Public Sans at 1200×630,
not an approximation that drifts from the page the moment either changes. The
two are deliberately siblings — same masthead, same two-column grid, same
footer rule — and differ in which of the site's own artefacts they carry: the
front page shows the four things and the fee, the audit shows the ledger.

To rebuild either after changing a price or a line:

    chrome --headless=new --hide-scrollbars --force-device-scale-factor=2 \
           --window-size=1200,630 --virtual-time-budget=15000 \
           --screenshot=og-2x.png og-home-card.html
    magick og-2x.png -resize 1200x630 -strip og-home.png

Rendered at 2× and downsampled, because text rasterised straight to 1200 wide
is visibly softer. Chrome needs a short working path — it fails to write the
file from a deep one — and `--virtual-time-budget` is what gives the webfonts
time to arrive; without it the card renders in Georgia and Arial.

Both cards carry prices: £450 on the front-page card, and £2,250 / £950 /
£1,300 on the audit card, which are the audit's own defaults at £150/hr.
Changing a tier price in `index.html` makes both wrong, and nothing will say
so. Rebuild them the same day.

Crawlers cache hard. A link already pasted somewhere will keep showing the old
preview until that cache expires; LinkedIn's Post Inspector forces a refresh.
