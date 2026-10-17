# Escape Away

Independent static homepage for https://escape-away.co.uk. Oast Cottage's existing repository and Stockholm Amplify app are unchanged.

## Preview
Open index.html in your browser. All images and styling are included locally. No package installation, API keys, cookies or analytics are required.

## GitHub and AWS Amplify
1. Create a separate GitHub repository named escape-away.
2. Upload the CONTENTS of this folder at the repository root (index.html, assets/, amplify.yml, robots.txt, sitemap.xml and this README). Do not upload the ZIP itself.
3. In AWS Amplify, Europe (Stockholm), create a new app for this new repository and its main branch. This is the intentional homepage deployment; keep the existing Oast Cottage app dyo7xsmu4qtz running.
4. Use the included amplify.yml. This is static HTML, not Next.js; output is the repository root and no npm command is needed.
5. Test the provided Amplify URL before connecting a custom domain.
6. The parent domain escape-away.co.uk is currently associated with the Oast Cottage app for its oastcottage subdomain. Do not delete or move that working association casually. Check Amplify's existing domain mappings before attaching the parent domain to this new app; it may require coordinated domain-association changes or using a new www mapping. DNS alone does not add a hostname to Amplify. We should complete this step together after the new app is tested.
7. Preserve the Cloudflare oastcottage CNAME and AWS certificate-verification CNAME; use DNS-only for AWS records.

## Content and assets
- Oast Cottage explore: https://oastcottage.escape-away.co.uk/
- Oast Cottage reviews: https://oastcottage.escape-away.co.uk/reviews
- Sykes reservations: exact listing URLs supplied by the owner, references 1068731 and 1057348.
- Windwhistle quotation and additional review text supplied by the owner, preserved verbatim.
- Oast Cottage headline is an exact sentence excerpt from the existing repository's src/lib/reviews.ts, featured entry 38. No personal guest names are published here.
- Actual property photographs downloaded from the owner's supplied Sykes listings. Source URLs are in ASSET-SOURCES.md; owner should ensure they have permission to reuse listing photography.

## Editing
Text, links and CSS are in index.html. Replace assets/oast-cottage.jpg or assets/windwhistle.jpg to change photography. Keep descriptive alt text up to date.
