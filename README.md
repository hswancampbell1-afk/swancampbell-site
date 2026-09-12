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
