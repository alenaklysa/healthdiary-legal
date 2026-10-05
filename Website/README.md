# HealthDiary public website

Static public pages for HealthDiary in English, Russian, German, and Ukrainian. The site uses only HTML and CSS: no build process, dependencies, CDN, cookies, analytics, forms, storage, iframe, or third-party script.

The legal text is a working template, not individual legal advice. Complete every placeholder, compare every product claim with the release build, and obtain an appropriate legal review before publication.

## Structure

```text
Website/
├── index.html
├── privacy-policy.html (compatibility redirect)
├── terms-of-use.html (compatibility redirect)
├── support.html (compatibility redirect)
├── privacy/index.html
├── terms/index.html
├── support/index.html
├── ru/index.html
├── ru/privacy/index.html
├── ru/terms/index.html
├── ru/support/index.html
├── de/index.html
├── de/privacy/index.html
├── de/terms/index.html
├── de/support/index.html
├── uk/index.html
├── uk/privacy/index.html
├── uk/terms/index.html
├── uk/support/index.html
├── assets/css/styles.css
├── assets/images/favicon.svg
├── 404.html
├── robots.txt
├── sitemap.xml
└── README.md
```

All internal URLs are relative, so the site works both at a GitHub Pages project path such as `https://username.github.io/healthdiary/` and from a local web server.

## Local preview

From the repository root:

```sh
python3 -m http.server 8000 --directory Website
```

Open `http://localhost:8000/`. A local server is preferred to double-clicking files because it reproduces trailing-slash page URLs and the GitHub Pages routing model.

## Placeholder inventory

Do not invent replacement values.

| Placeholder | Meaning | Files |
|---|---|---|
| `[DEVELOPER_NAME]` | Legal name of the responsible developer | Legal and localized pages |
| `[LEGAL_ENTITY_OR_BRAND]` | Legal entity or legally usable brand | Content-page footers |
| `[SUPPORT_EMAIL]` | Public support mailbox | Legal and support pages |
| `[PRIVACY_CONTACT_EMAIL]` | Public privacy mailbox | Privacy and support pages |
| `[DEVELOPER_COUNTRY]` | Country used after legal review | Privacy and Terms |
| `[EFFECTIVE_DATE]` | Publication/effective date | Privacy and Terms |
| `[APP_STORE_URL]` | Final App Store product URL | EN/RU home pages |
| `[GITHUB_PAGES_BASE_URL]` | Full base URL without a trailing slash | All EN/RU content pages, `robots.txt`, `sitemap.xml` |

Find every unresolved placeholder:

```sh
rg -n '\[[A-Z0-9_]+\]' Website
```

Replace the base URL in canonical and Open Graph metadata, `robots.txt`, and `sitemap.xml`. For a GitHub project site it will usually look like `https://username.github.io/healthdiary`.

## Link and source checks

Quick checks available on macOS:

```sh
find Website -type f | sort
rg -n 'href="/|src="/' Website
rg -n 'https?://' Website
rg -n 'script|iframe|localStorage|document\.cookie|analytics|tracker|cdn' Website
```

The only intentional external URL in page content is Apple’s Standard EULA. Canonical, Open Graph, sitemap, and robots URLs remain placeholders until publication.

Before publishing, use a link checker or browse every route in both languages. Confirm that EN/RU switches open the equivalent page, keyboard focus is visible, text remains readable at increased browser zoom, and the layouts work at 320, 375, 768, and 1440 CSS pixels in light and dark mode.

## Free publication with GitHub Pages

Publication is intentionally not performed by this project.

1. Create or choose a public GitHub repository only after approval.
2. Put the contents of `Website/` at the publishing source (for example, a repository root or a `docs/` directory). Do not copy the iOS project into the website publishing folder.
3. In GitHub repository Settings → Pages, choose “Deploy from a branch,” then select the correct branch and folder.
4. Wait for the Pages URL, replace `[GITHUB_PAGES_BASE_URL]`, and repeat all checks.
5. Verify that canonical URLs and the sitemap use the final HTTPS address.

For a custom domain later, add the domain in GitHub Pages settings, configure the DNS records GitHub documents for that domain, enable HTTPS after GitHub validates it, and update every base-URL placeholder. Add a `CNAME` file only when the domain is known.

## App Store Connect URLs

After replacing the base URL:

```text
Marketing URL:       [GITHUB_PAGES_BASE_URL]/
Privacy Policy URL:  [GITHUB_PAGES_BASE_URL]/privacy/
Terms of Use URL:    [GITHUB_PAGES_BASE_URL]/terms/
Support URL:         [GITHUB_PAGES_BASE_URL]/support/
```

The short route URLs above are canonical. The `.html` URLs are included for compatibility with the page names in the source text and redirect to their canonical equivalent.

English is the primary App Store-facing version. Russian, German, and Ukrainian equivalents are under `/ru/`, `/de/`, and `/uk/`.

## Security notes

GitHub Pages controls the response headers and does not provide full per-site HTTP-header configuration. Do not claim that a Content Security Policy is active unless the deployed response proves it.

If the site later moves to a configurable host, consider testing these headers before enabling them:

```text
Content-Security-Policy: default-src 'self'; img-src 'self'; style-src 'self'; script-src 'none'; object-src 'none'; base-uri 'self'; form-action 'none'; frame-ancestors 'none'; upgrade-insecure-requests
Referrer-Policy: strict-origin-when-cross-origin
X-Content-Type-Options: nosniff
Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=()
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

HSTS should be enabled only on a host that is permanently HTTPS-ready. Recheck CSP if scripts, forms, images, a custom domain, or other resources are added.

## Product claims verified against the current code

The local source review found:

- a local SwiftData store with iOS complete file protection;
- optional app protection through iOS device-owner authentication;
- user-requested, read-only access to supported HealthKit categories;
- an option to replace scheduled notification detail with generic text;
- temporary PDF file protection and cleanup;
- local Apple Vision OCR for supported lab PDFs and images;
- password-based authenticated encryption for new backup files;
- an iCloud account-status check, but no claim of active CloudKit database synchronization;
- no third-party analytics SDK, advertising SDK, or tracking permission flow in the reviewed project source.

## Confirm before publication

- Replace every placeholder with an accurate, public value.
- Confirm the legal developer/entity name, country, contacts, and effective date.
- Confirm that the App Store release build matches the reviewed source.
- Recheck all Apple Health categories, permissions text, and import behavior.
- Recheck notification privacy behavior, including already delivered notifications.
- Confirm PDF protection, cleanup, sharing warnings, and the fact that exported ordinary PDFs are not document-encrypted.
- Confirm backup encryption, password requirements, restore behavior, and safety-backup behavior.
- Confirm data deletion scope and that Apple Health originals are not deleted.
- Re-scan dependencies and network code for analytics, advertising, tracking, or server transfers.
- Confirm CloudKit synchronization is still not presented as active unless it is truly implemented and the policy is updated.
- Verify that no secrets or personal/medical data exist in website sources.
- Test all links, EN/RU pairs, keyboard navigation, 200% zoom, requested viewport sizes, and both color schemes.
- Review the English version as the App Store source of truth.
- Obtain legal review appropriate to the developer and target countries.
