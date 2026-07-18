# Brenden Butler Family Foundation (BBFF) Website

Static website for the Brenden Butler Family Foundation, a 501(c)(3) nonprofit (EIN: 92-1113183) based in DFW, Texas. The foundation supports pediatric cancer patients and their families through holiday gift drives, mental health advocacy, and adaptive athletics.

Live site: https://bbff1.github.io/BBFF/ (GitHub Pages, pending custom domain)

## Pages

| File | Purpose |
|---|---|
| `index.html` | Main site: mission, story, impact, executive board, donation section |
| `volunteer.html` | Student chapters: high school program, volunteer roles, chapter application |

Both pages are self-contained. All CSS and JavaScript are inline; the only external dependency is Google Fonts. Images live in `images/`.

## Hosting

The site is hosted on GitHub Pages from the `main` branch, root folder. Every push to `main` redeploys the site automatically within a minute or two.

To run locally:

```sh
python3 -m http.server 8090
# then open http://localhost:8090
```

## Custom domain (Wix)

Domain: `brendenbutlerfamilyfoundation.com`, purchased through Wix and using Wix nameservers (`ns2.wixdns.net`, `ns3.wixdns.net`; not editable, and no change needed). DNS records are edited in the Wix dashboard under Domains, then Manage DNS Records. There are no MX records on the domain, so the cutover cannot affect email; the foundation uses Gmail.

Current records (verified 2026-07-18), pointing at Wix hosting:

| Type | Host | Value | TTL |
|---|---|---|---|
| A | apex | 185.230.63.171 | 1 hour |
| A | apex | 185.230.63.186 | 1 hour |
| A | apex | 185.230.63.107 | 1 hour |
| CNAME | www | cdn1.wixdns.net | 1 hour |

Target records for GitHub Pages:

| Type | Host | Value | TTL |
|---|---|---|---|
| A | apex | 185.199.108.153 | 1 hour |
| A | apex | 185.199.109.153 | 1 hour |
| A | apex | 185.199.110.153 | 1 hour |
| A | apex | 185.199.111.153 | 1 hour |
| CNAME | www | bbff1.github.io | 1 hour |

Cutover order matters. Do not change DNS until steps 1 and 2 are done, or the domain will serve errors:

1. Enable GitHub Pages on this repo (Settings, then Pages: deploy from `main`, root). Requires admin on the repo.
2. In the same Pages settings, set the custom domain to `brendenbutlerfamilyfoundation.com`. GitHub commits a `CNAME` file to the repo and provisions a certificate.
3. In Wix, delete the three 185.230.63.x A records and add the four 185.199.108-111.153 A records. Edit the `www` CNAME value from `cdn1.wixdns.net` to `bbff1.github.io`.
4. Wait for propagation (TTL is 1 hour, so typically under an hour or two), then turn on "Enforce HTTPS" in the Pages settings.

The old Wix site stays intact in the Wix account; reverting DNS to the current records above rolls everything back.

## Donations (Stripe)

The donate button on `index.html` routes to a Stripe Payment Link (one-time gifts). The selected designation (Greatest Need, Gift Drive, Mental Health, Adaptive Athletics) is passed to Stripe as `client_reference_id`, and `thanks.html` is the post-payment landing page: set the link's after-payment behavior in Stripe to redirect to `https://brendenbutlerfamilyfoundation.com/thanks.html`.

Live link (one-time): https://buy.stripe.com/28E5kDf6S1lXbY0dJCfEk00

Still to do:
- Recreate or edit the link with "customer chooses price" so donors can give any amount (it currently charges a fixed $25)
- Create a monthly recurring Payment Link and paste it into `STRIPE_LINK_MONTHLY` in `index.html`, then re-enable the Monthly toggle
- Finish Stripe account verification (dashboard shows "review in progress")
- Apply for nonprofit pricing: email nonprofit@stripe.com with the EIN and IRS determination letter

## Contributing

1. Clone the repo and edit the HTML files directly.
2. Test locally (see Hosting above) before pushing.
3. Push to `main` to deploy.

Internal planning documents (playbooks, strategy guides, spreadsheets) are intentionally excluded from this repo via `.gitignore`. Keep them out of version control.

## Contact

- Email: brendenbutlerfamilyfoundation@gmail.com
- Instagram: [@brendenbutlerfamilyfoundation](https://www.instagram.com/brendenbutlerfamilyfoundation)
