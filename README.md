# Passport, visa and ID photo requirements by country

Open data on the photo rules for **155 passport, visa and ID documents in 52 countries**: printed size, digital file size, head height, background colour, expression, glasses, children, photo age, and whether a photo taken at home is accepted. Every record links to the source it was taken from and carries the date it was last checked.

- `data/photo-requirements.csv`: one row per document, flat columns
- `data/photo-requirements.json`: the same records with nested fields and the full list of sources

Browse the same data as a table: **[ovalight.com/en/photo-requirements](https://ovalight.com/en/photo-requirements/)**. It is also available in Spanish, Portuguese, German, French, Turkish, Russian and Arabic.

## Most common printed sizes

| Size | Documents |
|---|---:|
| 35 × 45 mm | 56 |
| 2 × 2 in (51 × 51 mm) | 9 |
| 40 × 60 mm | 7 |
| 30 × 40 mm | 5 |
| 50 × 70 mm | 3 |
| 35 × 50 mm | 3 |
| 50 × 60 mm | 3 |
| 33 × 48 mm | 2 |

108 of the 155 documents accept a photo you take yourself. For the others, the photo is taken at the office when you apply, or the authority asks for a professional photographer.

## Fields (CSV)

| Column | Meaning |
|---|---|
| `id` | Stable record id, e.g. `us-passport`, `eu-schengen-visa` |
| `country_code`, `country` | ISO 3166-1 alpha-2 code and English name (`EU` / Schengen Area for the Schengen visa) |
| `document` | Document name as the authority uses it |
| `page_url` | Human-readable page for this document |
| `print_width_mm`, `print_height_mm` | Printed photo size; `print_width_in`, `print_height_in` when the authority states inches |
| `digital_width_px`, `digital_height_px`, `digital_min_px`, `digital_max_px` | Pixel size or limits for an online upload |
| `digital_aspect`, `digital_min_kb`, `digital_max_kb`, `digital_formats` | Aspect ratio, file size limits (1 MB = 1000 KB unless the source gives exact bytes) and accepted formats |
| `head_height_mm_min/max`, `head_height_pct_min/max` | Head height from chin to crown, in mm on the print or % of the photo height |
| `background`, `background_hex` | Allowed background colours |
| `max_photo_age_months` | How recent the photo must be |
| `home_photo_accepted` | `yes` / `no` / `unknown`: whether a self-taken photo is accepted |
| `photo_capture` | `self`, `office` (taken when you apply), `professional` or `unknown` |
| `print_requirement` | `photo_paper_recommended`, `lab_print_only` or `not_applicable` |
| `confidence` | `high`: every rule confirmed on the source. `medium`: some details unpublished or ambiguous. `low`: no official page could be read |
| `verified_on` | Date the record was last checked against its source |
| `source_url`, `source_publisher` | The main source (the JSON lists all sources) |

Empty cells mean the authority does not publish that value. Ranges use an empty bound when only one side is published.

## Example

```python
import csv
rows = list(csv.DictReader(open("data/photo-requirements.csv", encoding="utf-8")))
uk = next(r for r in rows if r["id"] == "gb-passport")
print(uk["print_width_mm"], uk["print_height_mm"], uk["background"])  # 35 45 cream; light grey; …
```

## How it is maintained

Each record summarises what the issuing authority publishes on its website, in its forms or in its regulations. A monthly automated check reads every source page and flags changes, and the affected records are checked again. The record's `verified_on` date shows when it was last checked. This repository mirrors the files published at `https://ovalight.com/data/photo-requirements.{csv,json}`.

The official source always prevails. Rules change; check the linked source before you apply.

Found an error or a newer rule? Open an issue with the document and a link to the official page.

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may use, share and adapt the data, including commercially, with attribution:

> Source: Ovalight (ovalight.com), passport, visa and ID photo requirements, CC BY 4.0

Published by [Ovalight](https://ovalight.com/), a service for making compliant passport and visa photos with your phone.
