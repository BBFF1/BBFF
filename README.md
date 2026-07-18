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

The foundation's domain is managed through Wix. To point it at GitHub Pages:

1. In the Wix dashboard, open Domains, then Manage DNS Records for the domain.
2. Replace the existing A records for the apex domain with GitHub Pages' four IPs:
   - 185.199.108.153
   - 185.199.109.153
   - 185.199.110.153
   - 185.199.111.153
3. Add or update the `www` CNAME record to point to `bbff1.github.io`.
4. In the GitHub repo, go to Settings, then Pages, and enter the custom domain. This creates a `CNAME` file in the repo.
5. Wait for DNS to propagate (minutes to a few hours), then enable "Enforce HTTPS" in the Pages settings.

Domain: _to be filled in_
DNS status: _to be filled in_

## Donations (Stripe)

The donate form on `index.html` is currently a front-end mock. It does not process payments yet. The plan is to wire the amount buttons to Stripe Payment Links (one link per tier, plus recurring monthly variants). Stripe offers discounted nonprofit pricing; apply with the foundation's EIN.

Status: not yet configured.

## Contributing

1. Clone the repo and edit the HTML files directly.
2. Test locally (see Hosting above) before pushing.
3. Push to `main` to deploy.

Internal planning documents (playbooks, strategy guides, spreadsheets) are intentionally excluded from this repo via `.gitignore`. Keep them out of version control.

## Contact

- Email: brendenbutlerfamilyfoundation@gmail.com
- Instagram: [@brendenbutlerfamilyfoundation](https://www.instagram.com/brendenbutlerfamilyfoundation)
