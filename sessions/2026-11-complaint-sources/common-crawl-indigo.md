# Common Crawl as a free complaint index: IndiGo proof

Task: topc-social/wtf-tasks#13 · Researched 2026-10-26

## Bottom line

From one complaint site (consumercomplaints.in) and 20 Common Crawl snapshots (Jun 2024 to Oct 2026), the CDX index alone gave **46,666 unique complaint links**, with no request to the site itself and no cost. Each URL already carries the brand and the complaint's title, e.g. `indigo-airlines-my-baggage-broken-beyond-repairs-c3512756`, so link + brand + title come without opening a page.

For IndiGo specifically it's small: **24 links** with "indigo" in them (all airlines together: 278). Common Crawl samples a site, it doesn't mirror it: complaint ids in our links run from 857,329 to 3,545,245, so the site holds millions of complaints and we see roughly 1–2% of them.

So the approach works and is free, but one site via URL lists gives tens of thousands of links overall and dozens per brand, not 10,000s per brand. The ways to grow it are below.

## What was done

1. Listed crawls from `https://index.commoncrawl.org/collinfo.json` and took the latest 30.
2. For each: `GET https://index.commoncrawl.org/<crawl>-index?url=www.consumercomplaints.in/*&output=json&fl=url,timestamp,status`, up to 5 retries. 20 answered, 10 kept returning 504 (the public index server is overloaded at times).
3. Kept status 200 captures matching `/<slug>-c<id>`, de-duplicated by URL.

Captures per crawl ranged from 338 to 11,956.

| | Count |
|---|---|
| Unique complaint links | 46,666 |
| By capture year | 2024: 10,624 · 2025: 29,808 · 2026: 6,234 |
| Links with "indigo" | 24 |
| Links naming an airline (indigo, spicejet, air-india, akasa, vistara, go-first/goair) | 278 |
| Most frequent first word of the slug | reliance 384, bajaj 383, flipkart 367, big 358, tata 313, jaquar 302, hero 289, airtel 253 |

The first slug word is a rough brand guess ("the", "india", "big" are not brands); a real brand match needs a brand list.

## Sample IndiGo links (from the crawl index)

- https://www.consumercomplaints.in/indigo-airlines-damaged-luggage-indigo-c3520174
- https://www.consumercomplaints.in/indigo-airlines-delayed-service-c3537832
- https://www.consumercomplaints.in/indigo-airlines-full-refund-c3523444
- https://www.consumercomplaints.in/indigo-airlines-last-minute-made-to-give-cabin-luggage-for-cargo-hold-c3517041
- https://www.consumercomplaints.in/indigo-airlines-missing-connection-flights-and-financial-loss-due-to-the-unexpected-delay-in-flights-c3511796
- https://www.consumercomplaints.in/indigo-airlines-my-baggage-broken-beyond-repairs-c3512756
- https://www.consumercomplaints.in/indigo-airlines-non-receipt-of-refund-for-the-pnr-no-zl2mjb-c3500675
- https://www.consumercomplaints.in/indigo-airlines-regarding-cancellation-of-flights-and-then-not-providing-proper-solution-c3491626
- https://www.consumercomplaints.in/indigo-airlines-rude-behavior-of-indigo-supervisor-c1386373
- https://www.consumercomplaints.in/indigo-airlines-unable-to-generate-travel-certificate-c3512429
- https://www.consumercomplaints.in/indigo-airlines-voucher-issue-c3467728
- https://www.consumercomplaints.in/indigo-airlines-formal-complaint-unauthorized-booking-cancellation-without-notification-in-violation-of-consumer-rights-c3515560
- https://www.consumercomplaints.in/indigo-airlines-less-refund-ofticket-canceled-due-to-flight-delayof-indigo-flight-dt-19062015-c1102603
- https://www.consumercomplaints.in/indigo-airlines-refund-request-for-failed-booking-c3509427
- https://www.consumercomplaints.in/indigo-airlines-inconvenience-caused-and-financial-loss-in-modifying-the-flight-booking-c1167820
- https://www.consumercomplaints.in/makemytrip-makemytrip-is-not-refunding-my-cancelled-indigo-flight-money-c3542499
- https://www.consumercomplaints.in/ixigo-refund-against-pnr-no-sme1ye-indigo-flight-dated-04-12-2025-c3538302
- https://www.consumercomplaints.in/one97-communications-refund-from-indigo-airlines-c3475288

Checked from the URL slugs only, not by opening each page. Not all are complaints against IndiGo itself: `indigo-airlines-fraud-email-and-job`, `indigo-airlines-job-for-money` and `indigo-airlines-money-fraud` look like scams using IndiGo's name, and the MakeMyTrip, ixigo and Paytm ones are against the booking site. A brand match needs the first slug segment (the company the complaint is filed against), not "contains indigo".

## How it grows

- **More crawls.** Only 20 of ~110 crawls (back to 2008) were read; the 10 that 504'd and every older one can be retried. Union grows with each.
- **Brand listing pages from the archived copy.** Common Crawl also stores brand pages like `/1win-b116120/page/8`, each listing many complaints. Reading those from Common Crawl's own WARC files (`data.commoncrawl.org`, free range requests) multiplies links per brand without touching the site.
- **More sites.** MouthShut has captures in Common Crawl (CDX answered with 2 blocks for CC-MAIN-2025-43, not yet pulled). complaintboard.in had none in that crawl. Reddit, forums, Google Maps reviews: Reddit is in Common Crawl, X and Instagram mostly aren't.
- **Bulk instead of the API.** The CDX server is slow and flaky. Common Crawl also publishes the same index as Parquet files that can be filtered by domain with DuckDB; heavier download, no rate limits.

## Limits

- We store links, brand and a summary; the complaint text stays on its site. Showing the slug title is a few of the complainant's words, like a search result title.
- consumercomplaints.in's terms bar commercial use of its content (see `india-complaint-data.md`). Linking to it is a different act from republishing it, but selling a dataset built on it is the part to check with a lawyer before doing.
- Per-brand depth is the real gap: dozens of links per brand from this one site, not thousands.
