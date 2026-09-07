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
