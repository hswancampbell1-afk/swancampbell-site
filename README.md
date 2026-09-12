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

## The share card

`og-audit.png` is what LinkedIn, Slack and X render when someone pastes
`/audit`. It is a PNG because those crawlers will not render an SVG, which is
the one place on this site a raster file is unavoidable.

It is generated from `og-audit-card.html`, not drawn — the card is the site's
own CSS at 1200×630, so it uses the real Literata and Public Sans rather than
an approximation of them. To rebuild it after changing a price or a line:

    chrome --headless=new --hide-scrollbars --force-device-scale-factor=2 \
           --window-size=1200,630 --virtual-time-budget=15000 \
           --screenshot=og-2x.png og-audit-card.html
    magick og-2x.png -resize 1200x630 -strip og-audit.png

Rendered at 2× and downsampled, because text rasterised straight to 1200 wide
is visibly softer. Chrome needs a short path — it fails to write the file from
a deep one — and `--virtual-time-budget` is what gives the webfonts time to
arrive; without it the card renders in Georgia and Arial.

The figures on the card (£2,250, £950, £1,300) are the page's own defaults at
£150/hr. If the tier prices change in `index.html` they are wrong here too,
and nothing will say so.
