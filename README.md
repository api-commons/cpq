# Configure, Price, Quote

The common CPQ vocabulary -- the sales quotes reps build, the line items priced on them and the price books those prices come from -- distilled from the APIs that already exist. Products belong to commerce, deals to CRM and invoices to billing. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged CPQ, Configure Price Quote, Quoting, Sales Quotes, Proposals, Quote Management, Revenue Operations in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| sales_quote | 16 | 16 | id 69%, status 62% | quotes 13, quote 5, proposal 2, proposals 1 |

Cohort: 46 providers with harvested OpenAPI, 16 crosswalks. Of the providers exposing a sales_quote: 88% create, 56% list, 75% fetch, 50% update, 31% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A sales quote agrees only on id and status: total, discount, expiry and the deal it belongs to are each carried by a minority. Quotes are built inside CRM and CPQ suites and exposed as documents more than as structured records.
- Quote lines and price books are almost never resources in published APIs (2 and 1 providers).

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Quotes are `/sales-quotes`: insurance and market data own `/quotes`. Proposals count.
- Products are commerce's, deals CRM's, and invoices billing's.
- Quote lines and price books were measured and dropped.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
