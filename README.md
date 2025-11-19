# JSON-LD Structured Data Snippets

This folder contains initial JSON-LD snippets for Nares Law Group pages: homepage, Denver & Aurora location service pages, and core practice area pages.

## How to Use
1. Embed each file's JSON inside a `<script type="application/ld+json">` tag on its corresponding page.
2. Keep a single canonical Organization / LegalService node (homepage graph) or ensure identical `@id` values (`https://www.nareslawgroup.com/#org`) so Google merges them.
3. Do NOT duplicate large identical graphs across every page; location and practice pages here are starting points. You can streamline by loading only their page-specific `Service`, `WebPage`, and `BreadcrumbList` while allowing the Organization to come from a site-wide include.
4. Replace placeholder values: founder name, foundingDate, logo/image URLs, address, geo coordinates, phone, social profiles, publication dates.
5. If multiple office addresses exist, add additional `Place` / `LegalService` nodes with unique `@id`s (e.g. `#denver-office`, `#aurora-office`).

## Validating Your Structured Data
You can validate your JSON-LD snippets using these official tools:

1.  **Google Rich Results Test**: [https://search.google.com/test/rich-results](https://search.google.com/test/rich-results)
    *   **Purpose**: Checks if your page is eligible for Google's rich results (e.g., FAQ, Breadcrumbs).
    *   **What to Expect**: This tool will only report on schema types that can generate a rich result. It may show "2 valid items" (like `FAQPage` and `BreadcrumbList`) even if your graph contains more nodes like `Service` or `WebPage`, because those other nodes don't produce rich results on their own. This is normal.

2.  **Schema Markup Validator**: [https://validator.schema.org/](https://validator.schema.org/)
    *   **Purpose**: Validates the syntax and structure of your entire schema graph.
    *   **What to Expect**: This tool will show all parsed nodes from your graph (`Organization`, `LegalService`, `WebPage`, etc.), confirming that the structure is correct and all entities are recognized, regardless of whether they qualify for a rich result. Use this to check for overall correctness.

### Example Embed
Paste the JSON from the appropriate file into a script tag in the page `<head>` (or just before `</body>`):

```html
<script type="application/ld+json">

</script>
```

Tip: Keep JSON valid (no trailing commas, double quotes around keys/strings) and ensure `@id` values match across pages so Google can connect your entities.