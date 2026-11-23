# Strings Shopify supplies itself

Some storefront labels do not come from the theme's `locales/et.json` but from Shopify's own platform translations, which have no Estonian. On an Estonian storefront they stay in English whatever the theme file says:

- **Sort options** (`results.sort_options[].name`)
- **Availability filter values** ("In stock", "Out of stock")

The fix is a small snippet that prints an Estonian label when the storefront language is Estonian, and Shopify's own label otherwise.

## Sort options

| Sort value | English (Shopify) | Estonian |
|---|---|---|
| `manual` | Featured | Esiletõstetud |
| `most-relevant` | Most relevant | Kõige asjakohasemad |
| `relevance` | Relevance | Asjakohasus |
| `best-selling` | Best selling | Enim müüdud |
| `title-ascending` | Alphabetically, A-Z | Tähestiku järgi, A–Ü |
| `title-descending` | Alphabetically, Z-A | Tähestiku järgi, Ü–A |
| `price-ascending` | Price, low to high | Hind, madalamast kõrgemani |
| `price-descending` | Price, high to low | Hind, kõrgemast madalamani |
| `created-ascending` | Date, old to new | Kuupäev, vanemast uuemani |
| `created-descending` | Date, new to old | Kuupäev, uuemast vanemani |

(The Estonian alphabet ends in Ü, hence A–Ü.)

`snippets/sort-label-et.liquid`:

```liquid
{%- liquid
  assign label = option.name
  if request.locale.iso_code == 'et'
    case option.value
      when 'manual'
        assign label = 'Esiletõstetud'
      when 'most-relevant'
        assign label = 'Kõige asjakohasemad'
      when 'relevance'
        assign label = 'Asjakohasus'
      when 'best-selling'
        assign label = 'Enim müüdud'
      when 'title-ascending'
        assign label = 'Tähestiku järgi, A–Ü'
      when 'title-descending'
        assign label = 'Tähestiku järgi, Ü–A'
      when 'price-ascending'
        assign label = 'Hind, madalamast kõrgemani'
      when 'price-descending'
        assign label = 'Hind, kõrgemast madalamani'
      when 'created-ascending'
        assign label = 'Kuupäev, vanemast uuemani'
      when 'created-descending'
        assign label = 'Kuupäev, uuemast vanemani'
    endcase
  endif
  echo label
-%}
```

In Horizon, `snippets/sorting.liquid` prints `option.name` in several places (the list and the current choice); replace each with `{% render 'sort-label-et', option: option %}`.

## Availability filter

| Value | English (Shopify) | Estonian |
|---|---|---|
| `1` | In stock | Laos saadaval |
| `0` | Out of stock | Laost otsas |

`snippets/filter-label-et.liquid`:

```liquid
{%- liquid
  assign label = value.label
  if request.locale.iso_code == 'et' and filter.param_name == 'filter.v.availability'
    case value.value
      when '1'
        assign label = 'Laos saadaval'
      when '0'
        assign label = 'Laost otsas'
    endcase
  endif
  if escape
    echo label | escape
  else
    echo label
  endif
-%}
```

In Horizon, use it where filter values are printed: the checkbox label in `snippets/list-filter.liquid` and the active-filter pills in `snippets/filter-remove-buttons.liquid` (`{% render 'filter-label-et', filter: filter, value: value %}` instead of `value.label`; add `escape: true` where the original output was escaped).

Editing theme snippets means theme updates will not apply cleanly to those files; keep a note of the change.
