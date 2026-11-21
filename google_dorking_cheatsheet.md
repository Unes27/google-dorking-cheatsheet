# Google Dorking & Search Operators Cheat Sheet

> A practical reference for focused Google searches, public information research, and defensive review of websites you own or are authorized to assess. Google does not publish a complete list of every query pattern people call a “dork”; undocumented behavior can change.

**Last checked:** 2026-11-21  
**Example domain:** `example.com` — replace it with a domain you own or have written permission to review.

## Responsible use

- Use domain-scoped audit queries only on sites you own or are explicitly authorized to assess.
- Search results are clues about what Google may have indexed. A result does not grant permission to access, download, test, or share the underlying content.
- Do not use this sheet to seek credentials, tokens, personal data, private records, or access to systems you do not own.
- If you find unintended sensitive content on your own site, restrict or remove it at the source first. Search index controls are not access controls.
- For a site you own, use Search Console for URL-level checks and indexing reports. A `site:` search is incomplete and is not an authoritative inventory.

## Contents

1. [Quick start](#quick-start)
2. [Operator reference](#operator-reference)
3. [Useful query patterns](#useful-query-patterns)
4. [Google Images operators](#google-images-operators)
5. [Combining and troubleshooting queries](#combining-and-troubleshooting-queries)
6. [Retired and unreliable operators](#retired-and-unreliable-operators)
7. [A safe review workflow](#a-safe-review-workflow)
8. [Official references](#official-references)

## Quick start

Start with a domain and add one refinement at a time:

```text
site:example.com
site:example.com filetype:pdf
site:example.com "your public product name"
site:https://example.com/docs/ "installation"
```

Keep the operator attached to its value: `site:example.com` works; `site: example.com` does not. Google may return different results by location, language, time, and query wording.

## Operator reference

### Current, documented search refinements

| Syntax | What it does | Example |
|---|---|---|
| `"phrase"` | Looks for an exact phrase. | `site:example.com "annual report"` |
| `-word` | Excludes a word or phrase. | `site:example.com product -careers` |
| `site:domain` | Limits results to a domain, subdomain, URL, or URL prefix. | `site:example.com` |
| `filetype:pdf` | Requests results of a file type. | `site:example.com filetype:pdf` |
| `before:YYYY-MM-DD` | Looks for content Google dates before the given date. | `site:example.com before:2024-01-01` |
| `after:YYYY-MM-DD` | Looks for content Google dates after the given date. | `site:example.com after:2025-01-01` |

For a date interval, combine `after:` and `before:`. Date interpretation can be approximate; verify important results directly.

`site:` can take a URL prefix as well as a domain:

```text
site:https://example.com/docs/
site:https://example.com/products/widget
```

Google says `site:` results are not guaranteed to be exhaustive. A missing result does not prove that a URL is not indexed. For a site you manage, use Search Console's URL Inspection and indexing reports.

### Commonly used refinements that may vary

These are widely used in search examples, but Google’s current public operator reference does not document all of them. Test them with a simple query and treat results as approximate.

| Syntax | Common use | Example |
|---|---|---|
| `intitle:word` | Search for a word in a result title. | `site:example.com intitle:guide` |
| `inurl:word` | Search for a word in a result URL. | `site:example.com inurl:blog` |
| `intext:word` | Search for a word in page text. | `site:example.com intext:accessibility` |
| `allintitle: words` | Commonly used to require several title terms. | `site:example.com allintitle: product guide` |
| `allinurl: words` | Commonly used to require several URL terms. | `site:example.com allinurl: products help` |
| `allintext: words` | Commonly used to require several page-text terms. | `site:example.com allintext: shipping returns` |
| `OR` | Commonly used to search for either term; write it in uppercase. | `site:example.com pricing OR plans` |
| `*` | Sometimes used as a word placeholder inside a quoted phrase. | `site:example.com "built for * teams"` |
| `AROUND(n)` | Sometimes used to find terms near each other. | `site:example.com performance AROUND(3) report` |
| `n..m` | Sometimes used for numeric ranges. | `site:example.com model 2022..2025` |

Google may ignore or reinterpret these refinements. Parentheses are not a dependable way to group complex Boolean expressions; split a complicated query into smaller searches.

## Useful query patterns

Every example below is scoped to `example.com`. Replace it with an authorized domain before running a site review.

### 1. Review pages Google associates with a site

```text
site:example.com
site:https://example.com/help/
site:example.com "your organization name"
site:example.com "old product name"
```

Use the results to spot unexpected, stale, duplicate, or off-brand public pages. Search results do not provide a complete URL list.

### 2. Inventory intentionally public documents

Run one file type at a time for clearer results:

```text
site:example.com filetype:pdf
site:example.com filetype:docx
site:example.com filetype:xlsx
site:example.com filetype:pptx
site:example.com filetype:csv
site:example.com filetype:xml
```

Review whether each result is meant to be public and current. Do not use document searches to collect private or personal information.

### 3. Find older or dated public content

```text
site:example.com before:2024-01-01
site:example.com after:2025-01-01
site:example.com "old campaign name"
site:example.com "discontinued product name"
```

Use this for content maintenance and brand cleanup. Google's dates may not match the actual publication or update date.

### 4. Check for non-production pages on your own domain

`inurl:` is commonly used for these checks and may vary:

```text
site:example.com inurl:staging
site:example.com inurl:dev
site:example.com inurl:test
```

If a non-production result appears, verify ownership and secure the environment through normal access controls. Removing a result from Search alone does not protect a page.

### 5. Check for public directory listings on your own domain

`intitle:` behavior may vary:

```text
site:example.com intitle:"index of"
```

Review only systems you are authorized to assess. If a directory listing is unintended, disable it at the server or hosting configuration.

### 6. Find placeholder and maintenance copy

```text
site:example.com "under construction"
site:example.com "coming soon"
site:example.com "lorem ipsum"
site:example.com "replace this text"
```

These searches can help find unfinished public pages before or after a launch.

### 7. Review a topic or phrase on your site

```text
site:example.com accessibility
site:example.com "shipping and returns"
site:example.com -careers
site:example.com "support hours" before:2025-01-01
```

Use terms that are safe to search and intended for publication. Exact-phrase and exclusion searches are useful for content audits.

### 8. Research public sources by topic

Use a specific public institution or publication when you want focused research:

```text
site:who.int climate report filetype:pdf
site:docs.python.org "asyncio task"
site:example.edu marine biology
```

Check the source page, date, and context before citing or relying on a result.

## Google Images operators

Google documents these for Google Images specifically:

| Syntax | Use | Example |
|---|---|---|
| `imagesize:1200x800` | Find images of a specified dimension. | `site:example.com imagesize:1200x800` |
| `src:URL` | Find images that reference a particular image URL. | `src:https://example.com/images/logo.png` |

These do not work as general web-search filters. Availability and result behavior can vary.

## Combining and troubleshooting queries

1. Start with one broad query such as `site:example.com`.
2. Add one supported refinement, such as `filetype:pdf` or an exact phrase.
3. If results are too narrow, remove one term or run a separate query.
4. If results are noisy, add an exact phrase or exclude a clearly irrelevant term with `-word`.
5. Try a URL prefix when you are reviewing one section, for example `site:https://example.com/docs/`.
6. Open only pages you are authorized to access. Search operators do not bypass authentication or access controls.
7. For an owned site, confirm important findings in Search Console; use the live page and site configuration to determine actual access and status.

## Retired and unreliable operators

- **`cache:`** no longer works in Google Search.
- **`related:`** was removed from Google's search-operator documentation as unsupported.
- **`link:`**, **`info:`**, and many other lists copied online may be obsolete or unreliable. Do not rely on them without checking current behavior.
- **`intitle:`**, **`inurl:`**, `OR`, wildcards, and proximity syntax are commonly circulated but are not all included in Google's current public operator reference. Results can vary.

Google's documented operator set is selective. This cheat sheet separates documented refinements from commonly used patterns so readers can judge reliability.

## A safe review workflow

For an authorized site review:

1. Write down the exact domains and URL prefixes in scope.
2. Run domain-scoped searches and record the query, date, result URL, and why it needs review.
3. Confirm each result against the live site and the site's owner or administrator.
4. If content should not be public, restrict or remove it at the source, then use the appropriate Search Console controls to address search visibility.
5. Share only the minimum information needed to report a finding. Do not copy sensitive page contents into a public issue, spreadsheet, or repository.

## Official references

- [Refine Google searches](https://support.google.com/websearch/answer/2466433) — Google's documented popular refinements and syntax notes.
- [Debugging with Google Search operators](https://developers.google.com/search/docs/monitor-debug/search-operators) — documented `site:`, `filetype:`, and Google Images operators; notes that search operators have indexing and retrieval limits.
- [`site:` search operator](https://developers.google.com/search/docs/monitor-debug/search-operators/all-search-site) — URL-prefix searches and limitations of `site:` results.
- [Google Search Central documentation updates](https://developers.google.com/search/updates) — records the removal of `cache:` and `related:` guidance.
