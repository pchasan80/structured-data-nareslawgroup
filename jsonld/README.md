# JSON-LD Structured Data Snippets

This folder contains initial JSON-LD snippets for Nares Law Group pages: homepage, Denver & Aurora location service pages, and core practice area pages.

## How to Use
1. Embed each file's JSON inside a `<script type="application/ld+json">` tag on its corresponding page.
2. Keep a single canonical Organization / LegalService node (homepage graph) or ensure identical `@id` values (`https://www.nareslawgroup.com/#org`) so Google merges them.
3. Do NOT duplicate large identical graphs across every page; location and practice pages here are starting points. You can streamline by loading only their page-specific `Service`, `WebPage`, and `BreadcrumbList` while allowing the Organization to come from a site-wide include.
4. Replace placeholder values: founder name, foundingDate, logo/image URLs, address, geo coordinates, phone, social profiles, publication dates.
5. If multiple office addresses exist, add additional `Place` / `LegalService` nodes with unique `@id`s (e.g. `#denver-office`, `#aurora-office`).

## Validation Checklist
- Run each snippet in Google's Rich Results Test & Schema.org validator.
- Confirm no critical warnings: missing `name`, `url`, or invalid `@context`.
- Ensure `@id` patterns are consistent and stable (never auto-generate on deploy).
- Breadcrumb item order matches actual navigation.
- `inLanguage` should match page language variant (e.g. `en-US`).

## Recommended Enhancements (Optional)
- Add `FAQPage` JSON-LD if page content contains expandable Q&A.
- Add `Review` / `AggregateRating` only if genuine, verifiable reviews exist (avoid synthetic/inferred data).
- Include `LocalBusiness` subtype `Attorney` for office-specific contact pages.
- Integrate `ContactPoint` objects for different intake channels (e.g. phone, chat) under Organization.

## Reviews & Ratings (GBP)
- Policy: Google generally does not show review stars for self-serving reviews on `Organization`/`LocalBusiness` (incl. `LegalService`) entities even if you add markup. Your GBP rating may still appear in the local pack/knowledge panel, independent of on-page JSON-LD.
- Safe use: You can still include `AggregateRating` and individual `Review` objects for completeness and other consumers. Only mark up reviews that are visible on the page and that you have permission to publish. Do not mark up ratings sourced solely from third-party sites if you don’t show them on the page.
- Implementation: We added placeholders on the homepage Organization node. Update `ratingValue`, `ratingCount`, `reviewCount`, and insert a few real review snippets in `review`.
- Alternative: If you maintain page-specific reviews (e.g., for a service page), attach `aggregateRating`/`review` to that `Service` node—again, only when the same reviews are visibly present on that page.
- Source linking: Keep a `url` to the GBP profile and consider noting `publisher: { name: "Google" }` when the review originated there and is reproduced on your site.

## Performance & Maintenance
- Centralize the main Organization graph (e.g. in a PHP partial) and inject page-specific JSON-LD by concatenating an array then `json_encode`.
- Version control changes; treat structured data like an API contract.
- When adding new practice areas, clone a similar `Service` file adjusting `name`, `serviceType`, `description`, and `@id`.

## Example PHP Include (Conceptual)
```php
$org = json_decode(file_get_contents(__DIR__ . '/jsonld/homepage.jsonld'), true);
$service = json_decode(file_get_contents(__DIR__ . '/jsonld/denver-motor-vehicle-accident.jsonld'), true);
// Merge selective nodes: keep only Organization from homepage for other pages
$filteredOrg = array_filter($org['@graph'], fn($n) => in_array('Organization', (array)$n['@type']) || in_array('LegalService', (array)$n['@type']));
$otherNodes = $service['@graph'];
$graph = array_merge($filteredOrg, $otherNodes);
echo '<script type="application/ld+json">' . json_encode(['@context' => 'https://schema.org', '@graph' => $graph], JSON_UNESCAPED_SLASHES | JSON_UNESCAPED_UNICODE) . '</script>';
```

## Key Principles
- Accuracy over keyword stuffing.
- Stable identifiers.
- Minimal duplication.
- Reflect real visible content.

## Next Steps
Supply real firm data (address variants, geo coords, reviews, FAQs) to refine these snippets. Then re-run validation.
