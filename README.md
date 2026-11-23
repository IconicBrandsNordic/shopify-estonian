# Shopify in Estonian (eesti keel)

Free, native-reviewed Estonian translations of Shopify's standard storefront labels, ready to drop into a store.

Shopify ships no Estonian for its own themes (Horizon, Dawn) and Estonian is not one of the pre-translated checkout languages. Every Estonian store has to translate the same few hundred labels ("Add to cart", "Sort by", "Your cart is empty"...) itself. This pack does that once, properly, for everyone.

## What is in it

| Path | What | Status |
|---|---|---|
| [`horizon/4.1.4/et.json`](horizon/4.1.4/et.json) | Horizon theme storefront strings | 297 / 297 keys |
| [`horizon/4.5.0/et.json`](horizon/4.5.0/et.json) | Horizon theme storefront strings | 296 / 324 keys, missing ones listed in [`MISSING.md`](horizon/4.5.0/MISSING.md) (they show in English until added) |
| [`glossary.md`](glossary.md) | Terms and conventions used, plus common mistakes in other Estonian Shopify translations | |
| [`platform-strings.md`](platform-strings.md) | Sort and filter names Shopify supplies itself (no Estonian), and how to show them in Estonian | |
| `checkout/` | Checkout, order status and system messages | Coming (in review) |

Every string is in live use on a Shopify store and has been reviewed by native Estonian speakers. Tone is informal (*sina*), the usual choice for Estonian online shops.

Not included: theme editor (admin) strings (`et.schema.json`), merchant content (menus, pages, sections) and product data.

## How to use it

**Theme files (Shopify CLI or GitHub integration)**

1. Find your Horizon version: Online Store > Themes > the theme's "..." menu, or `theme_version` in `config/settings_schema.json`.
2. Copy `horizon/<that version>/et.json` to your theme's `locales/et.json`. If your exact version is missing, use the nearest lower one; keys that do not exist in your theme are simply ignored.
3. Push the theme. Add and publish Estonian under Settings > Languages if you have not already.

**Without code:** Online Store > Themes > "..." > Edit default theme content, switch the language to Estonian and copy the strings you need from the file.

Already translated some labels yourself? Merge rather than overwrite: anything you changed in the language editor lives in the same `locales/et.json`.

## Corrections and new versions

Spotted a wrong or awkward translation, or need a newer Horizon version? Open an issue with the key, the current text and your suggestion. Corrections are checked by a native reviewer before they are merged.

## Credits

- Translations: [Iconic Brands Nordic OÜ](https://github.com/IconicBrandsNordic), Tallinn.
- Native review: **Kadri-Liis Viil** and **Laura Jaakson**.

## Licence

The Estonian translations, glossary and documentation are licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE): use them in any store, commercial or not, and change them freely; please credit "Iconic Brands Nordic OÜ - github.com/IconicBrandsNordic/shopify-estonian" somewhere sensible (a code comment is fine).

The translation keys and English source strings belong to Shopify Inc. and come from the Horizon theme; see [`NOTICE`](NOTICE). This pack is a translation for use with Shopify themes and is not affiliated with or endorsed by Shopify.
