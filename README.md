# swancampbell.co.uk

The practice's one-page site. Static HTML, no build step, no dependencies —
edit `index.html` and push; GitHub Pages redeploys in about a minute.

`CNAME` holds the custom domain and is what tells Pages to serve it there.
Deleting it silently reverts the site to the github.io address.

Deliberately one page. A site does not win clients — conversations do — and
this exists so that a prospect who has already been pitched can look the
practice up and find something that reads as real.

Three claims on it are load-bearing and must stay true: that nothing goes out
in your name without you approving it, that drafts may appear before they have
been reviewed, and that on Microsoft 365 sending permission is only requested
if you switch on automatic invoice reminders — until then, the consent screen
does not include sending. All three are properties of the software behind the
service, not aspirations. If any stops being true, this page changes the same
day.

The first has one narrow exception, approved 5 October 2026. Replies are
drafted, never sent. Calendar invitations go only when you press the button.
Invoice reminders are drafts too by default; if you switch that on and approve
the wording first, that approved reminder can be sent. Nothing else can.

The third is the one most easily broken by accident, because it lives in
another repository. Until automatic invoice reminders are switched on, it is
true because `MICROSOFT_SCOPES["email"]` in the control panel is `Mail.Read`,
`Mail.ReadWrite`, `User.Read` — creating a draft and sending one are separate
permissions in Microsoft Graph, and only the first is held. Adding `Mail.Send`
to that default set would make the "until then" sentence on this page false
without anyone touching this repository. Switching the reminders on is a
reconnect, so Microsoft grants sending then and not before.

Note what the page does *not* claim. Google's `gmail.compose` is described by
Google as "manage drafts and send emails", so on Google the permission would
allow sending and only the software prevents a reply or an invitation from
going out. The one send the software will make is an invoice reminder, and
only after you switch that on and approve the wording. The page says so. The
admission is why the Microsoft half is worth believing.

The commercial offer changed on 5 October 2026. The public packages are
Inbox Starter (setup and the first month), Back Office (monthly), and
Back Office+ (monthly, including six on-request jobs). One job is one
clear deliverable, about 20–30 minutes, not an ongoing project. Extras are
£15 each, and anything bigger needs a written yes first.
Founding prices are locked for 12 months, there are five founding places,
and a 50% deposit secures one. The audit prices one person's week against
those three founding fees. It does not pool several people into one fee,
and the site must not grow a pooled tier back unless the offer itself
changes. Contact on every page is hswancampbell1@gmail.com.

The drafted-reply specimens, added 13 September 2026 (the front
page's Tom and the audit's Marion) say they are exactly what the software
writes. That is true because the draft composer in `vatools` is told never to
invent facts, dates or commitments that were not in the email it answers, and
to write a bracketed placeholder instead - and `draftcheck.py` flags a reply
that introduces a date or figure the incoming email did not contain. Every
word outside a bracket in both specimens must be traceable to the incoming
email shown above it. The first versions of both were not: they invented a
delivery time, a warehouse delay, a Q3 headcount change, and a conclusion
about a client's banking covenant, which is the most dangerous sentence a
machine could draft for this audience and the one thing the software is
built never to write. If placeholders are ever filled from the client's own
mail, each filled value must show its source, and the specimens should only
change once that is built and verified - not before.

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
front page shows the founding prices, the audit shows the ledger.

To rebuild either after changing a price or a line:

    chrome --headless=new --hide-scrollbars --force-device-scale-factor=2 \
           --window-size=1200,630 --virtual-time-budget=15000 \
           --screenshot=og-2x.png og-home-card.html
    magick og-2x.png -resize 1200x630 -strip og-home.png

Rendered at 2× and downsampled, because text rasterised straight to 1200 wide
is visibly softer. Chrome needs a short working path — it fails to write the
file from a deep one — and `--virtual-time-budget` is what gives the webfonts
time to arrive; without it the card renders in Georgia and Arial.

Both cards carry prices. The front-page card shows the founding start price
and the two monthly founding fees. The audit card shows the audit's own
defaults at £150/hr: £2,250 of hours, the Back Office founding fee of £75,
and the £2,175 difference. Changing a tier price in `index.html` or in the
audit's `TIERS` makes both wrong, and nothing will say so. Rebuild them the
same day.

Crawlers cache hard. A link already pasted somewhere will keep showing the old
preview until that cache expires; LinkedIn's Post Inspector forces a refresh.
