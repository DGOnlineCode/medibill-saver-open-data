# MediBill Saver open data

MediBill Saver was a small tool that checked US hospital bills against public federal price data. It ran from April to September 2026 and has been shut down. Its maker would rather give the useful parts away than let them sit in a database, so here they are, free.

- **`itemized-bill-request-letter.txt`**: the free letter that asks a hospital billing office for a fully itemized bill under your HIPAA right of access (45 CFR 164.524). Fill in the [brackets] and send it in writing. General information, not legal advice.
- **`data/`**: the public price and hospital tables the tool used, as gzipped JSON Lines (one JSON object per line), exported 2026-09-27.

| File | Rows | Size |
|---|---|---|
| `data/cms_hospital_compare.jsonl.gz` | 319,285 | 2.0 MB |
| `data/cms_msdrg_definitions.jsonl.gz` | 770 | 0.0 MB |
| `data/cms_pfs_rates.jsonl.gz` | 9,499 | 0.1 MB |
| `data/cost_page_stats.jsonl.gz` | 7,173 | 1.6 MB |
| `data/data_sources.jsonl.gz` | 8 | 0.0 MB |
| `data/hospital_rates.jsonl.gz` | 1,313,081 | 10.1 MB |
| `data/hospitals_meta.jsonl.gz` | 5,426 | 0.3 MB |
| `data/irs_pub78.jsonl.gz` | 42,001 | 1.1 MB |

## What each table is

- `hospital_rates`: negotiated, cash and gross charge amounts per hospital (by NPI) and billing code, in cents, from hospitals' federally required price-transparency files (45 CFR 180.50). Each hospital is the originating publisher of its own figures.
- `cost_page_stats`: per-code summaries computed from `hospital_rates` (percentiles, medians, min/max, cheapest and priciest hospitals).
- `hospitals_meta`: hospital names, addresses, type and overall rating from CMS Care Compare.
- `cms_hospital_compare`: CMS Care Compare quality metrics per hospital.
- `cms_pfs_rates`: CMS Physician Fee Schedule national-average rates per billing code. Code descriptions are intentionally left out (CPT descriptors are AMA copyright).
- `cms_msdrg_definitions`: CMS MS-DRG definitions, weights and mean lengths of stay.
- `irs_pub78`: IRS Publication 78 tax-exempt organization list (used to spot nonprofit hospitals).
- `data_sources`: where every table came from, its license and attribution text.

## License and sources

The compilation and the computed summaries are released under **CC0 1.0** (public domain dedication). The underlying source data is public domain (US federal works: CMS, IRS) or hospitals' federally mandated public price postings; see `data/data_sources.jsonl.gz` for each source's license and attribution. No warranty: prices change, files have errors, and nothing here is medical, legal or financial advice. No personal data is included.

Made by LootCastPuff LLC. The story of why it closed: https://lootcastpuff.com/medibill-saver-joy-over-profit/
